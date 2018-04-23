<template>
    <div class="newslist">
        <ul>
            <li v-for="(art,index) in articles" :key="index">
                <div>
                    <a v-bind:href="art.url" target="_target">
                        <img v-bind:src="art.urlToImage">
                    </a>
                </div>
                <div>
                    <h4><a v-bind:href="art.url">{{art.title}}</a></h4>
                    <h5>by {{art.author}}</h5>
                    <p>{{art.description}}</p>
                </div>
            </li>
        </ul>
    </div>
</template>

<script>
import axios from 'axios';

export default {
    name: 'newslist',
    props: ['source'],
    watch: {
       source: function(val) {
           this.updateSource(val);
       }
    },
    data () {
        return {
            articles: []
        }
    },
    created: function() {
        this.updateSource(this.source);
    },
    methods: {
        updateSource: function(source) {
            // https://newsapi.org/v2/everything?q=bitcoin&apiKey=4d61abe798b149a0ab2685c68630c444
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
