<template>
<v-app>  
    <v-layout row wrap>
        <v-flex sm12 md-10 md-offset-1>
            <v-jumbotron color="grey lighten-2" >
                <v-container fill-height>
                    <v-layout align-center>
                        <v-flex>
                            <h3 class="display-3">News Feed - {{source.name}}</h3>
                            <div v-if="source">
                                <span class="subheading">{{source.description}}</span>
                                <v-divider class="my-3"></v-divider>
                                <div class="title mb-3">
                                    <a v-bind:href="source.url" target="_blank">Go to {{source.name}} website</a>
                                </div>
                            </div>
                            <v-menu offset-y>
                                <v-btn color="primary" dark slot="activator">Select other news source</v-btn>
                                <v-list>
                                    <v-list-tile v-for="source in sourceArr" :key="source.title" @click="sourceChanged(source.id)">
                                        <v-list-tile-title v-bind:value="source.id"> {{ source.name }}</v-list-tile-title>
                                    </v-list-tile>
                                </v-list>
                            </v-menu>
                        </v-flex>
                    </v-layout>
                </v-container>
            </v-jumbotron>
        </v-flex>
    </v-layout>
</v-app>
</template>

<script>
import axios from 'axios';

export default {
    name: 'sourceselection',
    data () {
        return {
            sourceArr: [],
            source: ''
        }
    },
    methods: {
        sourceChanged: function(id) {
            for (let index = 0; index < this.sourceArr.length; index++) {
                if(this.sourceArr[index].id === id) {
                    this.source = this.sourceArr[index];
                }       
            }
            this.$emit('sourceChanged', id);
        },
        chkSource() {
            for (let index = 0; index < this.sourceArr.length; index++) {
                if(this.sourceArr[index].id === 'bbc-news') {
                    this.source = this.sourceArr[index];
                }       
            }
        }
    },
    created: function() {
        axios.get('https://newsapi.org/v2/sources?language=en&apiKey=4d61abe798b149a0ab2685c68630c444')
        .then(response => {
            console.log('response:', response.data.sources);
            this.sourceArr = response.data.sources;
            this.chkSource();   
        });
        
    }
}
</script>

<style scoped>

</style>
