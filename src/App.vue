<template>
    <div id="app">
        <v-app light>
            <v-content>
                <v-container grid-list-md text-xs-center>
                    <v-layout row wrap align-center>
                        <v-flex xs12 md12>
                            <div class="text-xs-center">
                                <v-layout justify-space-between>
                                    <SourceSelection v-on:sourceChanged="sourceChanged"></SourceSelection>
                                </v-layout>
                            </div>
                        </v-flex>
                    
                        <!-- <v-flex xs12 md12> -->
                            <Post v-bind:source="source"></Post>
                            <!-- <NewsList v-bind:source="source"></NewsList> -->
                        <!-- </v-flex> -->
                    </v-layout>
                </v-container>
            </v-content>
        </v-app>
  </div>
</template>

<script>
import SourceSelection from './components/SourceSelection'
import NewsList from './components/NewsList'
import Post from './components/Post'

export default {
  name: 'App',
  components: {
    SourceSelection,
    NewsList,
    Post
  },
  data() {
    return {
      source: 'bbc-news',
      title: 'Your Logo'
      
    }
  },
  methods: {
    sourceChanged: function (source) {
        console.log(source);
      this.source = source;
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;

  padding-top: 20px;
}
</style>
