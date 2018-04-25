<template>
<v-app>
    <v-layout row wrap>
        <v-flex  v-for="(art,index) in articles" :key="index" xs12 sm4 md4 >
            <v-card hover>
                <v-card-media
                class="white--text empty-image"
                height="170px"
                :src="art.urlToImage"
                >
                </v-card-media>
                <v-container fill-height fluid>
                    <v-layout>
                    <v-flex xs12 align-end d-flex>
                        <span class="card-headline text-xs-left">
                            {{art.title}}
                        </span>
                    </v-flex>
                    </v-layout>
                </v-container>
                <v-card-text class="text-xs-left">
                    <div class="descr">{{art.description}}</div>
                </v-card-text>
                <v-card-actions>
                    <v-spacer></v-spacer>
                    <v-btn flat class="blue--text" v-bind:href="art.url">
                        Read More
                    </v-btn>
                </v-card-actions>
            </v-card>
        </v-flex>
    </v-layout>
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
                this.articles = response.data.articles;
            })
        }
    }
}
</script>

<style lang="scss" scoped>
div {
    &.descr {
        width:100%;
        text-align:justify;
        display: -webkit-box;  
        overflow:hidden;
        text-overflow : ellipsis;
        -webkit-line-clamp: 6;
        -webkit-box-orient: vertical;
        color: #6b6d6e;
        min-height: 11rem;
    }
}

.card-headline {
    width:100%;
    text-align:justify;
    display: -webkit-box;  
    overflow:hidden;
    text-overflow : ellipsis;
    -webkit-line-clamp: 2;
    -webkit-box-orient: vertical;
    font-size: 1.5rem;
    font-weight: 400;
    line-height: 2rem;
    letter-spacing: normal;
}

.empty-image {
    background-color: #455a64;
    background-image: url("../assets/404.png");
}
</style>