<template>
        <ion-card>
            <ion-card-header>
                <ion-card-title color="light">{{post.Title}}</ion-card-title>
                <ion-card-subtitle>{{movieDetails.Type}}</ion-card-subtitle>
                <ion-card-subtitle>{{movieDetails.Genre}}</ion-card-subtitle>
            </ion-card-header>
            <ion-card-content>
                <ion-img :src="image"></ion-img>
                <ion-item>
                    <ion-label>R: {{movieDetails.Rated}}, Released: {{movieDetails.Released}}</ion-label>
                </ion-item>
                <ion-card-content>
                    {{movieDetails.Plot}}
                </ion-card-content>
                <ion-card-content>
                    Cast: {{movieDetails.Actors}}
                </ion-card-content>
                <ion-button color="tertiary" expand="full" @click="goToHome()">Go back</ion-button>
            </ion-card-content>
        </ion-card>
</template>

<script>
import axios from 'axios';
export default {
    props: ['post', 'originalTitle'],
    data() {
        return {
            image: '',
            movieDetails: []
        }
    },
    async mounted() {
        const details = await axios.get('http://www.omdbapi.com/?apikey=981288&i=' + this.post.imdbID);
        this.image = details.data.Poster; 
        this.movieDetails = details.data;
    },
    methods : {
        goToHome() {
            let originalTitle = this.originalTitle;
            this.$router.push({name: 'home', params: { originalTitle }})
        }    
    }
}
</script>

