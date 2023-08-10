<template>
  <div
    :class="[
      imgClicked
        ? 'flex w-screen h-screen fixed z-30 top-0 bottom-0 right-0 left-0 bg-black bg-opacity-30 cursor-pointer'
        : 'hidden',
      'justify-center items-center',
    ]"
  >
    <img
      :src="imageUrl('/assets/' + project.image)"
      ref="img"
      @click.prevent="imgClicked = false"
      class="object-scale-down drop-shadow-xl w-full h-full sm:w-[80%] sm:h-[80%]"
    />
  </div>
  <div
    class="flex flex-col sm:flex-row w-full px-7 sm:p-0 sm:w-7/12 py-8 sm:py-10 border-top sm:border-none"
  >
    <div
      class="w-96 hidden sm:flex flex-none justify-center items-start cursor-pointer"
    >
      <img
        :src="imageUrl('/assets/' + project.image)"
        ref="img"
        @click.prevent="imgClicked = true"
      />
    </div>
    <div class="flex flex-col sm:ml-7 text-left">
      <h4
        class="text-lg font-semibold text-gray-400 tracking-wide"
        style="font-family: 'Quicksand', sans-serif"
      >
        {{ project.time }}
      </h4>
      <div class="flex flex-row mt-1 items-start">
        <h2
          class="text-xl font-semibold text-gray-700 tracking-wide"
          style="font-family: 'Quicksand', sans-serif"
        >
          {{ project.title }}
        </h2>

        <a
          :href="project.link"
          target="_blank"
          class="text-base sm:text-lg ml-3 pt-0.5 sm:pt-1 text-red-400 hover:text-red-300"
        >
          <fa :icon="['fas', 'external-link-alt']"></fa>
        </a>
      </div>
      <img
        :src="imageUrl('/assets/' + project.image)"
        class="w-full sm:hidden mt-3"
        ref="img"
        @click.prevent="imgClicked = true"
      />
      <p
        class="text-lg font-normal mt-3 text-gray-600 leading-snug tracking-normal"
        style="font-family: 'Quicksand', sans-serif"
      >
        {{ project.desc }}
      </p>
      <ul class="flex mt-5 flex-wrap tracking-wide">
        <li :key="tool.id" v-for="tool in project.tools">
          <div
            class="py-1 px-3 mb-2 mr-2 rounded-md border border-amber-400 text-amber-400 font-semibold text-xs"
            style="font-family: 'Quicksand', sans-serif"
          >
            {{ tool }}
          </div>
        </li>
      </ul>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref } from "vue";

defineProps<{
  project: any;
}>();

const imgClicked = ref(false);

function imageUrl(url: string) {
  const result = new URL(url, import.meta.url) as unknown;
  const returnResult = result as string;
  return returnResult;
}
</script>

<style scoped></style>
