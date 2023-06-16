<script>
import axios from 'axios';

export default {
    name: "PostList",
    data() {
        return {
            base_url: 'http://127.0.0.1:8000/',
            posts_API: 'api/posts',
            loading: true,
            posts: null,
            error: null,
            max_text_lenght: 100,
        }
    },
    methods: {
        getPosts(url) {
            axios
                .get(url)
                .then(response => {
                    //console.log(response);
                    this.posts = response.data.posts
                    this.loading = false
                })
                .catch(error => {
                    //console.log(error);
                    this.error = error.message
                })
        },
        getImageFromPath(path) {
            //console.log(this.base_url + 'storage/' + path);
            return this.base_url + 'storage/' + path;
        },
        prevPage(path) {
            console.log(path);
            this.getPosts(path);
        },
        nextPage(path) {
            //console.log(path);
            this.getPosts(path);
        },
        /**
         * 
         * @param {string} text the text to truncate
         */
        truncateText(text) {
            if (text.length > this.max_text_lenght) {
                //console.log(text.slice(0, 30));
                //console.log(text.substring(0, 30));
                return text.slice(0, this.max_text_lenght) + '...';
            }
            //console.log(text);
            return text
        }

    },
    mounted() {
        const url = this.base_url + this.posts_API
        console.log(url);
        this.getPosts(url)
    }
}
</script>

<template>
    <div class="p-5 mb-4 bg-light rounded-3">
        <div class="container-fluid py-5">
            <h1 class="display-5 fw-bold">My Blog</h1>
            <p class="col-md-8 fs-4">Lorem ipsum dolor sit amet consectetur adipisicing elit. Vel perspiciatis ducimus
                architecto adipisci deleniti quisquam, similique nulla ea in illo enim ratione provident iste voluptatem
                impedit eligendi est tempore beatae?</p>

        </div>
    </div>
    <section class="posts" v-if="posts && !loading">
        <div class="container">
            <div class="row row-cols-1 row-cols-sm-2 row-cols-md-3 row-cols-xl-4 g-4">
                <div class="col" v-for="post in posts.data">
                    <div class="card h-100">
                        <img class="card-img-top" :src="getImageFromPath(post.cover_image)" alt="">
                        <div class="card-body">

                            <h3>
                                {{ post.title }}
                            </h3>
                            <p>
                                {{ truncateText(post.content) }}
                            </p>
                            <router-link :to="{name: 'single-post', params: {'slug': post.slug}}">Read more</router-link>
                        </div>
                        <div class="card-footer">
                            <span class="badge bg-primary">{{ post.id }}</span>
                        </div>

                    </div>
                </div>


            </div>

            <nav aria-label="Page navigation" class="py-4 text-center">
                <ul class="pagination    ">
                    <li class="page-item">
                        <button class="page-link" aria-label="Previous" v-if="posts.prev_page_url"
                            @click="prevPage(posts.prev_page_url)">
                            <span aria-hidden="true">&laquo;</span>
                        </button>
                    </li>
                    <li class="page-item">
                        <button class="page-link" aria-label="Next" v-if="posts.next_page_url"
                            @click="nextPage(posts.next_page_url)">
                            <span aria-hidden="true">&raquo;</span>
                        </button>

                    </li>
                </ul>
            </nav>
        </div>
    </section>
    <div v-else>
        <section class="loading">
            <div class="container">
                <div class="row">
                    <div class="col">
                        <div class="card" aria-hidden="true">
                            <img src="http://127.0.0.1:8000/storage/placeholders/d25732475395f314d6188347134a8321.jpg"
                                class="card-img-top">
                            <div class="card-body">
                                <h5 class="card-title placeholder-glow">
                                    <span class="placeholder col-6"></span>
                                </h5>
                                <p class="card-text placeholder-glow">
                                    <span class="placeholder col-7"></span>
                                    <span class="placeholder col-4"></span>
                                    <span class="placeholder col-4"></span>
                                    <span class="placeholder col-6"></span>
                                    <span class="placeholder col-8"></span>
                                </p>
                                <a href="#" tabindex="-1" class="btn btn-primary disabled placeholder col-6"></a>
                            </div>
                        </div>
                    </div>
                    <div class="col">
                        <div class="card" aria-hidden="true">
                            <img src="http://127.0.0.1:8000/storage/placeholders/d25732475395f314d6188347134a8321.jpg"
                                class="card-img-top">
                            <div class="card-body">
                                <h5 class="card-title placeholder-glow">
                                    <span class="placeholder col-6"></span>
                                </h5>
                                <p class="card-text placeholder-glow">
                                    <span class="placeholder col-7"></span>
                                    <span class="placeholder col-4"></span>
                                    <span class="placeholder col-4"></span>
                                    <span class="placeholder col-6"></span>
                                    <span class="placeholder col-8"></span>
                                </p>
                                <a href="#" tabindex="-1" class="btn btn-primary disabled placeholder col-6"></a>
                            </div>
                        </div>
                    </div>
                    <div class="col">
                        <div class="card" aria-hidden="true">
                            <img src="http://127.0.0.1:8000/storage/placeholders/d25732475395f314d6188347134a8321.jpg"
                                class="card-img-top">
                            <div class="card-body">
                                <h5 class="card-title placeholder-glow">
                                    <span class="placeholder col-6"></span>
                                </h5>
                                <p class="card-text placeholder-glow">
                                    <span class="placeholder col-7"></span>
                                    <span class="placeholder col-4"></span>
                                    <span class="placeholder col-4"></span>
                                    <span class="placeholder col-6"></span>
                                    <span class="placeholder col-8"></span>
                                </p>
                                <a href="#" tabindex="-1" class="btn btn-primary disabled placeholder col-6"></a>
                            </div>
                        </div>
                    </div>
                    <div class="col">
                        <div class="card" aria-hidden="true">
                            <img src="http://127.0.0.1:8000/storage/placeholders/d25732475395f314d6188347134a8321.jpg"
                                class="card-img-top">
                            <div class="card-body">
                                <h5 class="card-title placeholder-glow">
                                    <span class="placeholder col-6"></span>
                                </h5>
                                <p class="card-text placeholder-glow">
                                    <span class="placeholder col-7"></span>
                                    <span class="placeholder col-4"></span>
                                    <span class="placeholder col-4"></span>
                                    <span class="placeholder col-6"></span>
                                    <span class="placeholder col-8"></span>
                                </p>
                                <a href="#" tabindex="-1" class="btn btn-primary disabled placeholder col-6"></a>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </section>
    </div>
</template>

<style lang="scss" scoped></style>