<script lang="ts" setup>
import sdk, { EmbedOptions } from "@stackblitz/sdk";

/* sdk.embedProjectId("embed", "css-custom-prop-color-values", {
  openFile: "index.ts",
}); */

const embed = ref(null);

watchEffect(() => {
  if (embed.value) {
    embed.value.appendChild(document.createElement("div"));
    sdk.embedProjectId(embed.value.children[0], "css-custom-prop-color-values");
  }
});
</script>

<template>
  <client-only>
    <div ref="embed" id="embed"></div>
  </client-only>
</template>

<style lang="postcss" scoped></style>
