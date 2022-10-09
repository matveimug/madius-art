<script setup>
import { ref } from "vue";
import VueEasyLightbox from "vue-easy-lightbox";

const visibleRef = ref(false);
const indexRef = ref(0);
let imgs = Object.keys(import.meta.glob("../public/imgs/*"));
imgs = imgs.map(x => x.replace(/\/public/g,""));
const showImg = (index) => {
  indexRef.value = index;
  visibleRef.value = true;
};
const onHide = () => (visibleRef.value = false);
const name = (src) => src.split("/").pop();
</script>

<template>
  <main>
    <article
      v-for="(src, index) in imgs"
      :key="index"
      @click="() => showImg(index)"
    >
      <img :alt="name(src)" :src="src" />
    </article>
    <vue-easy-lightbox
      :visible="visibleRef"
      :imgs="imgs"
      :index="indexRef"
      @hide="onHide"
      :zoomScale="0.5"
    ></vue-easy-lightbox>
  </main>
</template>
