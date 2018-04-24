<template>
<v-app>
    <!-- <div v-for="post in posts" :key="post.title"> -->
    <!-- <div v-for="(art,index) in articles" :key="index"> -->
    <v-flex xs6 md4>
        <v-card hover  v-for="(art,index) in articles" :key="index">
            <v-card-media
            class="white--text"
            height="170px"
            :src="art.urlToImage"
            >
            <v-container fill-height fluid>
                <v-layout>
                <v-flex xs12 align-end d-flex>
                    <span class="headline">
                        <a v-bind:href="art.url">{{art.title}}</a>
                    </span>
                </v-flex>
                </v-layout>
            </v-container>
            </v-card-media>
            <v-card-text>
            {{art.description}}
            </v-card-text>
            <v-card-actions>
                <v-spacer></v-spacer>
                <v-btn flat class="blue--text">Read More</v-btn>
            </v-card-actions>
        </v-card>
    </v-flex>
    <!-- </div> -->
</v-app>
</template>

<script>
import axios from 'axios';

export default {
    props: ['source'],
    watch: {
       source: function(val) {
           this.updateSource(val);
       }
    },
    created: function() {
        this.updateSource(this.source);
    },
    data () {
        return {
            articles: []
        }
    },
    methods: {
        updateSource: function(source) {
            axios.get(`https://newsapi.org/v2/everything?q=${source}&apiKey=4d61abe798b149a0ab2685c68630c444`)
            .then(response => {
                console.log('response:', response);
                this.articles = response.data.articles;
            })
        }
    }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>