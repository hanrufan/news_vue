<template>
    <div class="sourceselection">
        <div>

            <h2>News List</h2>
            <h4>Select new source</h4>
        
            <select v-on:change="sourceChanged">
                <option v-bind:value="source.id" v-for="(source,index) in sourceArr" :key="index">
                    {{source.name}}
                </option>
            </select>

            <div v-if="source">
                <h6>{{source.description}}</h6>
                <a v-bind:href="source.url" target="_blank">Go to {{source.name}} website</a>
            </div>
        </div>
        <v-menu offset-y>
            <v-btn color="primary" dark slot="activator">News Feed</v-btn>
            <v-list>
                <v-list-tile v-for="source in sourceArr" :key="source.title" @click="newsChanged(source.id)">
                    <v-list-tile-title v-bind:value="source.id"> {{ source.name }}</v-list-tile-title>
                </v-list-tile>
            </v-list>
        </v-menu>
    </div>
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
        sourceChanged: function(e) {
             console.log('e:',e);
            for (let index = 0; index < this.sourceArr.length; index++) {
                if(this.sourceArr[index].id === e.target.value) {
                    this.source = this.sourceArr[index];
                }       
            }
            console.log('e.target.value:',e.target.value);
            this.$emit('sourceChanged', e.target.value);
        },
        newsChanged: function(id) {
             console.log('id:', id);
            for (let index = 0; index < this.sourceArr.length; index++) {
                if(this.sourceArr[index].id === id) {
                    this.source = this.sourceArr[index];
                }       
            }
            this.$emit('newsChanged', e.target.value);
        }
    },
    created: function() {
        axios.get('https://newsapi.org/v2/sources?language=en&apiKey=4d61abe798b149a0ab2685c68630c444')
        .then(response => {
            console.log('response:', response);
            this.sourceArr = response.data.sources;
        })
    }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
