<script lang="ts" setup>
import sdk, { EmbedOptions, VM, ProjectFiles } from "@stackblitz/sdk";
import type { StackBlitzPayloadOptions } from "../types/sb";
const { stackBlitzOption, exercice } = defineProps({
  exercice: {
    type: Object as PropType<StackBlitzPayloadOptions>,
    required: true,
  },
  stackBlitzOption: {
    type: Object as PropType<EmbedOptions>,
  },
});
/* sdk.embedProjectId("embed", "css-custom-prop-color-values", {
  openFile: "index.ts",
}); */

const embed = ref(null);
let vm: VM | null = null;
let files: ProjectFiles | null = null;
const test = computed(() => {
  if (files == null) return [];

  let r = JSON.parse(files["result.json"]);
  return r.testResults;
});
const testParsed = computed(() => {
  return test.value.length !== 0
    ? test.value.map((t: any) => {
        return t.assertionResults as any[];
      })
    : [];
});

watchEffect(async () => {
  if (embed.value) {
    embed.value.appendChild(document.createElement("div"));
    vm = await sdk.embedGithubProject(
      embed.value.children[0],
      exercice.github,
      stackBlitzOption
    );
    files = await vm.getFsSnapshot();
    if (vm !== null) {
      console.log("files", files);
      console.log("test", test.value);
      console.log("testParsed", testParsed.value);
    }
  }
});

watchEffect(() => {
  if (vm !== null) {
    console.log("ici");
    console.log("vm", vm);
    console.log("files", testParsed);
  }
});
</script>

<template>
  <client-only>
    <div ref="embed" id="embed"></div>
    <h2>Result</h2>
    <template v-if="testParsed.length !== 0">
      <ul>
        <li v-for="(t, i) in testParsed" :key="i">
          <p>{{ t.fullName }}</p>
        </li>
      </ul>
    </template>
  </client-only>
</template>

<style lang="postcss" scoped></style>
