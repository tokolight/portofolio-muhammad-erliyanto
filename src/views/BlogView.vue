<template>
  <div class="container mx-auto p-3 md:p-8">
    <div class="flex flex-col-reverse md:flex-row relative">
      <div class="w-full md:w-2/3">
        <div class="flex flex-col gap-4 md:px-20 fade-zoom-up">
          <article v-for="article in articles" :key="article.id">
            <router-link :to="`/soal/${article.slug}/${article.id}`" class="flex w-full bg-[#1e1e1f] border-[#383838] rounded-xl text-left text-white p-5 md:py-7 md:px-8 cursor-pointer hover:bg-[#282828] items-center">
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
export default {
  data() {
    return {
      articles: [
        {
          title: "Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed cursus.",
          desc: "Vestibulum auctor ullamcorper enim ut vestibulum...",
          slug: "excepturi-architecto-quos",
          image: "https://picsum.photos/600/450",
          date: "Mei 12, 2023",
          content: "Content 1",
          id: "1"
        },
        {
          title: "Etiam nec odio ligula. Cras fringilla mattis risus, id sollicitudin.",
          desc: "Donec eu orci a magna blandit fermentum...",
          slug: "nam-nam-consequuntur",
          image: "https://loremflickr.com/600/450/abstract",
          date: "Juni 25, 2023",
          content: "asdasda",
          id: "2"
        },
        {
          title: "Iusto pariatur aspernatur ducimus dolores voluptatum quibusdam similique.",
          desc: "Mollitia amet fuga repellat...",
          slug: "aspernatur-eos-perspiciatis",
          image: "https://loremflickr.com/640/480/abstract",
          date: "Thursday",
          content: "content 3",
          id: "3"
        },
        {
          title: "Qui molestiae consectetur sed.",
          desc: "Pariatur harum mollitia veritatis...",
          slug: "neque-dicta-eaque",
          image: "https://loremflickr.com/640/480/abstract",
          date: "Thursday",
          content: "content 4",
          id: "4"
        },
        {
          title: "Nihil alias laudantium facere itaque quasi veniam iste.",
          desc: "Voluptatibus eligendi sapiente molestias...",
          slug: "cumque-error-sapiente",
          image: "https://loremflickr.com/640/480/abstract",
          date: "Friday",
          content: "content 5",
          id: "5"
        },
        {
          title: "Minus iure molestiae libero reiciendis.",
          desc: "Sed omnis accusantium occaecati ratione...",
          slug: "ut-ad-consequuntur",
          image: "https://loremflickr.com/640/480/abstract",
          date: "Sunday",
          content: "content 6",
          id: "6"
        },
        {
          title: "Possimus fugiat optio.",
          desc: "Dicta consequatur blanditiis delectus nobis...",
          slug: "incidunt-hic-architecto",
          image: "https://loremflickr.com/640/480/abstract",
          date: "Tuesday",
          content: "content 7",
          id: "7"
        }
      ],
      blogview: []
    }
  },
  mounted() {
    this.populateBlogView();
  },
  methods: {
    populateBlogView() {
      this.blogview = this.articles.map(article => ({
        id: article.id,
        title: article.title,
        slug: article.slug,
        date: article.date
      }));
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
