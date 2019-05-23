<template>
    <div>
        <ion-item>
            <ion-input :value="title" @input="title = $event.target.value" pattern="search" placeholder="Enter your Movie or series name"></ion-input>
            <ion-icon name="search" size="large" slot="end" @click="searchData()"></ion-icon>
        </ion-item>
        <template v-if="posts.length != 0">
            <ion-card v-for="post in posts.data.Search" :key="post.imdbID" style="border: 1px solid gray;">
                <ion-card-content>
                    <template v-if="post.Poster.startsWith('https://')">
                        <img :src="post.Poster" alt="">
                    </template>
                        <ion-label color="light">{{post.Title}}, {{post.Year}}</ion-label>
                        <ion-button color="tertiary" expand="full" @click="viewMore(post)">View More</ion-button>
                </ion-card-content>
            </ion-card>
        </template>
    </div>
</template>

<script>
import axios from 'axios';
export default {
    data() {
        return {
            posts: [],
            title: ''
        }
    },
    async mounted() {
    },
    methods: {
        viewMore(post) {
            this.$router.push({name: 'detail', params: { post }})
        },
        async searchData() {
            this.posts = [];
            console.log('Searching data.....');
             const response = await axios.get('http://www.omdbapi.com/?apikey=981288&s=' + this.title)
            this.posts = response;
        }
    }
}
</script>
