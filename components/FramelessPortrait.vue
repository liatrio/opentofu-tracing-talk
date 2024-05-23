<!--
Profile Picture

Usage:

<Portrait src="/blair.png" name="Blair Drummond" title="DevOps Engineer"/>
-->

<script setup lang="ts">
defineProps<{
  src: string,
  name: string,
  title?: string,
  desc?: string,
  email?: string,
}>()
</script>

<template>
  <div class="slidev-layout flex grid image-x -mt-30 p-0 -ml-20" >
    <div class="my-auto flex rounded-2xl" style="transform: scale(0.5);">
      <div>
        <div class="rounded-2xl flex justify-center items-center p-8 object-cover" :class="imageOrder">
          <img :src=src style="border-radius:50%; border-color: grey; border-width: 1px;" />
        </div>
        <div class="flex -mt-8 justify-center items-center p-8 max-h-md object-cover">
          <h2> {{ name }} </h2>
        </div>
        <div class="flex -mt-20 justify-center items-center p-8 max-h-md object-cover" >
          <h3 style="font-weight: 100; text-align: center;"> {{ title }} </h3>
        </div>
        <div class="flex -mt-16 justify-center items-center p-8 max-h-md object-cover" >
          <p style="font-weight: 100;"> {{ desc }} </p>
        </div>
        <div class="flex -mt-16 justify-center items-center p-8 max-h-md object-cover" >
          <a href="mailto:{{ email }}" style="font-size: x-large;"> {{ email }} </a>
        </div>
      </div>
    </div>
  </div>
</template>
