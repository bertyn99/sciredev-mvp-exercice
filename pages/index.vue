<script lang="ts" setup>
import { StackBlitzPayloadOptions } from "~/types/sb";

let ex: StackBlitzPayloadOptions = {
  github: "bertyn99/sciredev-exercice/tree/main/exo1",
  openFile: "index.html",
};
</script>

<template>
  <div class="mx-auto max-w-7xl sm:px-6 lg:px-8">
    <h1>Course</h1>

    <p>
      Lorem ipsum, dolor sit amet consectetur adipisicing elit. Neque quasi
      aliquam doloribus tempore facere tenetur ullam vero ipsam provident
      temporibus iste incidunt consectetur harum omnis atque voluptate sed,
      optio suscipit!
    </p>
    <p>
      Lorem ipsum, dolor sit amet consectetur adipisicing elit. Neque quasi
      aliquam doloribus tempore facere tenetur ullam vero ipsam provident
      temporibus iste incidunt consectetur harum omnis atque voluptate sed,
      optio suscipit!
    </p>

    <ExerciceCanvas :exercice="ex" />
  </div>
</template>

<style lang="postcss" scoped></style>
