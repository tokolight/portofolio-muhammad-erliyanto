<template>
    <div class="w-full md:w-3/5 h-20 mx-auto md:mt-5">
        <div class="bg-white rounded-xl mx-3 p-5 md:p-10 md:mx-0" v-for="(article, index) in articles" :key="index">
            <div>
                <h1 class="text-xl md:text-4xl text-black text-left font-bold leading-relaxed">{{ article.title }}</h1>
                <div class="mt-3 text-left text-gray-800 text-sm">Published at <span>{{ article.date }}</span></div>
                <div class="h-[2px] w-20 my-5 md:my-10 bg-[#00FFFF] md:w-1/3 aos-init aos-animate mr-2"></div>
                <div>
                    <div class="relative w-full" style="padding-top: 50%;">
                        <img :src="article.image" class="absolute top-0 left-0 rounded-lg w-full h-full object-cover" alt="Thumbnail">
                    </div>
                </div>
                <div class="text-left text-black mt-8" v-html="article.content"></div>
            </div>
        </div>
    </div>
</template>

<script>
import axios from 'axios';

export default {
    data() {
        return {
            articles: [],
            urls: [
                'https://670fd6ada85f4164ef2c23b4.mockapi.io/api/blog/all',
                'https://670fd6ada85f4164ef2c23b4.mockapi.io/api/blog/2',
                'https://670fd6ada85f4164ef2c23b4.mockapi.io/api/blog/3',
                'https://670fd6ada85f4164ef2c23b4.mockapi.io/api/blog/4',
                'https://670fd6ada85f4164ef2c23b4.mockapi.io/api/blog/5'
            ]
        }
    },
    mounted() {
        this.getArticles();
    },
    methods: {
        async getArticles() {
            try {
                const requests = this.urls.map(url => axios.get(url));
                const responses = await Promise.all(requests);
                this.articles = responses.map(response => response.data);
            } catch (error) {
                console.error('Error fetching articles:', error);
            }
        }
    }
}
</script>

<style scoped></style>
