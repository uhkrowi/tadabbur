<template>
  <div class="h-screen3 w-full bg-white flex inline-flex shadow-md">
    <div id="sidenav" class="w-1/4 overflow-y-scroll custom-scroll p-5 text-lg">
      <div class="w-full flex justify-center mb-6">
        <img src="/img/quran.png" alt="quran.png" class="h-24">
      </div>
      <input list="browsers" class="w-full mb-4 pl-2" placeholder="Cari">
      <datalist id="browsers">
        <option v-for="(item, index) in suras" :key="index" :value="item.nama" @click="changeSurah(item)" />
      </datalist>
      <div v-for="(item, index) in suras" :key="index" class="mb-2 text-white flex justify-between cursor-pointer" @click="changeSurah(item)">
        <div class="flex inline-flex">
          <span>{{ index + 1 }}. &nbsp;</span>
          <div class="flex flex-col">
            <span>{{ item.nama }}</span>
            <small>({{ item.arti }})</small>
          </div>
        </div>
        <span>{{ item.asma }}</span>
      </div>
    </div>
    <!-- Content -->
    <div class="w-3/4">
      <div class="h-full overflow-y-scroll custom-scroll relative">
        <div class="bg-tertiary text-center p-2 sticky top-0 right-0 left-0">
          <div class="relative mb-1">
            <div>
              <span class="font-bold">
                {{ recentSurah.nama }} | {{ recentSurah.asma }}
              </span>
              <br>
              <small>({{ recentSurah.arti }})</small>
              <br>
              <div class="flex justify-end">
                <audio
                  :src="'https://cdnserver14.mp3quran.net/khalf/'+recentSurah.chapter+'.mp3'"
                  controls
                  class="h-8 shadow outline-none focus:outline-none active:outline-none"
                  style="background: #F1F3F4">
                </audio>
              </div>
            </div>
            <div class="absolute left-0 top-0">
              <small>Tipe: {{ recentSurah.type }}</small>
              <small>| Ayat: {{ recentSurah.ayat }}</small>
            </div>
          </div>
        </div>
        <div>
          <Surah :dataset="dataset" />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
import Surah from '~/components/Surah'

export default {
  components: {
    Surah
  },
  data () {
    return {
      recentSurah: {
        chapter: '001',
        nama: 'Al-Fatihah',
        arti: 'Pembukaan',
        asma: 'الفاتحة',
        ayat: '7',
        type: 'mekah'
      },
      suras: [],
      dataset: {
        ayas: []
      }
    }
  },
  watch: {
  },
  mounted () {
    this.fetchSurah()
    this.fetchSurahList()
  },
  methods: {
    async fetchSurahList () {
      try {
        const res = await axios.get('/raw/suras.json')
        this.suras = res.data
      } catch (e) {
        console.log(e)
      }
    },
    async fetchSurah () {
      try {
        const res = await axios.get(`https://api.mp3quran.net/api/surah?surah=${this.recentSurah.chapter}&language=id`)

        this.dataset.ayas = []
        setTimeout(() => {
          this.dataset.ayas = res.data
        }, 2000)
      } catch (e) {
        console.log(e)
        this.fetchSurah()
      }
    },
    changeSurah (surah) {
      let surahChapter = surah.nomor

      if (surah.nomor.length === 1) {
        surahChapter = '00' + surah.nomor
      } else if (surah.nomor.length === 2) {
        surahChapter = '0' + surah.nomor
      }

      this.recentSurah = {
        chapter: surahChapter,
        nama: surah.nama,
        asma: surah.asma,
        arti: surah.arti,
        ayat: surah.ayat,
        type: surah.type
      }

      this.fetchSurah()
    }
  }
}
</script>

<style>
@font-face {
  font-family: 'litelpmq';
  font-weight: normal;
  src: url('/font/litelpmq.woff2') format('woff2'),
       url('/font/litelpmq.woff2') format('woff');
}

* {
  font-family: 'litelpmq';
}

.font-ar {
  font-family: 'litelpmq';
}
</style>
