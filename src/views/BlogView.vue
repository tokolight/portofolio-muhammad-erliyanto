<template>
  <div class="container mx-auto p-3 md:p-8">
    <div class="flex flex-col-reverse md:flex-row relative">
      <div class="w-full md:w-2/3">
        <div class="flex flex-col gap-4 md:px-20 fade-zoom-up">
          <article v-for="article in articles" :key="article.id">
            <router-link :to="`/read/${article.slug}/${article.id}`" class="flex w-full bg-[#1e1e1f] border-[#383838] rounded-xl text-left text-white p-5 md:py-7 md:px-8 cursor-pointer hover:bg-[#282828] items-center">
              <div class="w-full pr-4">
                <div class="text-xs mb-1 text-slate-400 flex items-center italic">
                  <div class="h-[1px] w-20 bg-amber-200 md:w-5 aos-init aos-animate mr-2"></div> {{ article.date }}
                </div>
                <h1 class="text-sm md:text-md text-amber-200 font-bold mb-2 paraf">{{ article.title }}</h1>
                <div class="text-sm hidden md:block paraf">{{ article.desc }}</div>
              </div>
              <div>
                <div class="w-20 h-20 md:w-28 flex items-center md:h-28">
                  <img :src="article.image" class="rounded-lg md:rounded-xl" alt="">
                </div>
              </div>
            </router-link>
          </article>
        </div>
      </div>
      <div class="w-full md:w-1/3 h-fit p-8 md:sticky md:top-24">
        <!-- Sidebar -->
        <div class="flex flex-col text-left">
          <div class="bg-clip-text bg-gradient-to-r from-slate-100 to-amber-300 text-transparent">Let's share experiences,
            stories, and knowledge together.
          </div>
          <div class="h-[1px] mt-7 mb-7 w-20 bg-amber-200 aos-init aos-animate mr-2"></div>
          <div class="hidden md:block">
            <div class="text-white text-md font-semibold">Topics</div>
            <div class="mt-3 flex flex-wrap gap-1">
              <span class="py-2 px-3 rounded-2xl bg-[#1e1e1f] hover:bg-white/20 text-white text-xs cursor-pointer">NodeJS</span>
              <span class="py-2 px-3 rounded-2xl bg-[#1e1e1f] hover:bg-white/20 text-white text-xs cursor-pointer">Technology</span>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import ArticleList from '@/components/ArticleList.vue';
import axios from "axios";

export default {
  data() {
    return {
      articles: [],
      urls: [
        'https://64a38c9cc3b509573b564183.mockapi.io/api/blog/1',
        'https://telegra.ph/Tugas-ASJ-Ujian-Akhir-Bab-3-09-30',
        'https://telegra.ph/Tugas-ASJ-Ujian-Akhir-Bab-4-09-30',
        'https://telegra.ph/Tugas-ASJ-Ujian-Akhir-Bab-5-09-30'
      ]
    }
  },
  components: {
    ArticleList
  },
  mounted() {
    this.getArticles();
  },
  methods: {
    async getArticles() {
      try {
        const requests = this.urls.map(url => axios.get(url));
        const responses = await Promise.all(requests);
        
        this.articles = responses.map(response => {
          if (response.config.url.includes('telegra.ph')) {
            const parser = new DOMParser();
            const doc = parser.parseFromString(response.data, 'text/html');
            return {
              id: response.config.url, // Menggunakan URL sebagai ID sementara
              slug: '', // Ganti jika ada slug
              title: doc.querySelector('h1').innerText || 'No Title',
              date: new Date().toLocaleDateString(),
              desc: doc.querySelector('.tg') ? doc.querySelector('.tg').innerHTML : 'No Content',
              image: '' // Ganti jika ada gambar
            };
          } else {
            return response.data; // Mengambil data langsung dari API
          }
        });
      } catch (error) {
        console.error('Error fetching articles:', error);
      }
    }
  }
}
</script>

<style scoped>
.paraf {
  -webkit-line-clamp: 3;
  -webkit-box-orient: vertical;
  text-overflow: ellipsis;
  overflow: hidden;
}
@media (min-width: 768px) { 
  .paraf {
    display: -webkit-box;
  }
}
@keyframes fadeZoomUp {
  0% {
    opacity: 0;
    transform: scale(0.5);
  }
  100% {
    opacity: 1;
    transform: scale(1);
  }
}
.fade-zoom-up {
  animation: fadeZoomUp 1s ease-in-out;
}
</style>
