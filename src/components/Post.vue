<template>
<v-app>
    <v-layout row wrap>
    <v-flex  v-for="(art,index) in articles" :key="index" xs12 sm4 md4 >
        <v-card hover>
            <v-card-media
            class="white--text"
            height="170px"
            :src="art.urlToImage"
            >
            </v-card-media>
            <v-container fill-height fluid>
                <v-layout>
                <v-flex xs12 align-end d-flex>
                    <span class="headline text-xs-left">
                        <a v-bind:href="art.url">{{art.title}}</a>
                    </span>
                </v-flex>
                </v-layout>
            </v-container>
            <v-card-text class="text-xs-left ">
                <div class="descr">{{art.description}}</div>
            </v-card-text>
            <v-card-actions>
                <v-spacer></v-spacer>
                <v-btn flat class="blue--text">Read More</v-btn>
            </v-card-actions>
        </v-card>
    </v-flex>
    </v-layout>
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
        console.log('init post:', this.source);
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
                console.log(source, 'response:', response);
                this.articles = response.data.articles;
            })
        }
    }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
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
    }
}

</style>