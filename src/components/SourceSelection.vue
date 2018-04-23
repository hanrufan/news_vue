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
                <v-list-tile v-for="item in sourceArr" :key="item.title" @click="sourceChanged">
                    <v-list-tile-title v-bind:value="source.id">{{ item.name }}</v-list-tile-title>
                </v-list-tile>
            </v-list>
        </v-menu>

        <!-- <v-layout row>
            <v-list two-line>
                <template v-for="(item, index) in sourceArr">
                    <v-subheader v-if="item.header" :key="item.header">{{ item.header }}</v-subheader>
                    <v-divider v-if="index + 1 < item.length" :key="`divider-${index}`"></v-divider>
                    <v-list-tile avatar v-else :key="item.name">
                    <v-list-tile-avatar>
                      
                    </v-list-tile-avatar>
                    <v-list-tile-content>
                        <v-list-tile-title v-html="item.name"></v-list-tile-title>
                        <v-list-tile-sub-title v-html="item.description"></v-list-tile-sub-title>
                    </v-list-tile-content>
                    </v-list-tile>
                </template>
            </v-list>
        </v-layout> -->
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
            for (let index = 0; index < this.sourceArr.length; index++) {
                if(this.sourceArr[index].id === e.target.value) {
                    this.source = this.sourceArr[index];
                }       
            }
            console.log('e.target.value:',e.target.value);
            this.$emit('sourceChanged', e.target.value);
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
