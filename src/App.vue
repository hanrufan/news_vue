<template>
    <div id="app">
          <v-app light>
            <v-content>
            <v-container>
                <v-layout row wrap align-center>
                <!-- <v-flex xs12 md4>
                    <div class="text-xs-center">
                    <v-avatar size="125px">
                        <img
                        class="img-circle elevation-7 mb-1"
                        src="https://raw.githubusercontent.com/vuetifyjs/docs/dev/static/doc-images/lists/1.jpg"
                        >
                    </v-avatar>
                    <div class="headline">John <span style="font-weight:bold">Carter</span></div>
                    <div class="subheading text-xs-center grey--text pt-1 pb-3">Lorem ipsum dolor sit amet</div>
                    <v-layout justify-space-between>
                        <a href="javascript:;" class="body-2">Home</a>
                        <a href="javascript:;" class="body-2">About</a>
                        <a href="javascript:;" class="body-2">Github</a>
                        <a href="javascript:;" class="body-2">Other</a>
                    </v-layout>
                    </div>
                </v-flex> -->
                <v-flex xs12 md4>
                    <div class="text-xs-center">
                        <v-layout justify-space-between>
                            <SourceSelection v-on:sourceChanged="sourceChanged"></SourceSelection>
                        </v-layout>
                    </div>
                </v-flex>
                <v-flex xs12 md5 offset-md2>
                    <Post v-bind:source="source"></Post>
                    <!-- <NewsList v-bind:source="source"></NewsList> -->
                </v-flex>
                </v-layout>
            </v-container>
            </v-content>
        </v-app>

    <!-- <SourceSelection v-on:sourceChanged="sourceChanged"></SourceSelection>
    <NewsList v-bind:source="source"></NewsList> -->
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
