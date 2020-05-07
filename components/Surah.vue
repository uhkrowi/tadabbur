<template>
  <div>
    <div class="m-6 mr-8 ml-8">
      <!-- <img src="/img/bismillah.png" alt="/img/bismillah.png" class="mx-auto" style="zoom: 50%" /> -->
      <div class="mb-2 mx-auto text-center text-2xl mb-6">بِسْمِ اللّٰهِ الرَّحْمٰنِ الرَّحِيْمِ</div>
      <div class="mb-6 mx-auto text-center">Dengan nama Allah Yang Maha Pengasih, Maha Penyayang</div>
      <hr>
    </div>
    <div v-show="dataset.ayas.length !== 0" v-for="(item, index) in dataset.ayas" :key="index" class="m-6 mr-8 ml-8">
      <!-- <img :id="'ayah-'+(index)" :src="item.image_url.replace('http', 'https')" :alt="item.image_url" class="mx-auto mr-0" style="zoom: 45%" /> -->
      <div class="text-right text-2xl mb-6">{{ item.ayah_text }}</div>
      <div class="mb-6">{{ item.ayah_text_lang }}</div>
      <hr>
    </div>
    <div v-show="dataset.ayas.length === 0" v-for="(item, index) in 3" :key="index" class="m-6 mr-8 ml-8">
      <div class="line mx-auto mr-0 h-6 w-40 mb-3 rounded-full"></div>
      <div class="line mx-auto mr-0 h-6 w-64 mb-3 rounded-full"></div>
      <div class="line h-4 w-64 mb-3 rounded-full"></div>
      <div class="line h-4 w-40 mb-3 rounded-full"></div>
      <hr>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    dataset: {
      type: Object
    }
  }
}
</script>

<style scoped>
.line {
  background-image: linear-gradient(90deg, #ddd 0px, #e8e8e8 40px, #ddd 80px);
  background-size: 600px;
  animation: shine-lines 1.6s infinite linear;
}

@keyframes shine-lines {
  0% {
    background-position: -100px;
  }
  40%, 100% {
    background-position: 140px;
  }
}
</style>
