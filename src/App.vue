<template>
    <v-app light id="app">
        <v-content>
            <v-container grid-list-md text-xs-center>
                <SourceSelection v-on:sourceChanged="sourceChanged"></SourceSelection>
                <Post v-bind:source="source"></Post>
            </v-container>
        </v-content>
    </v-app>
</template>

<script>
import SourceSelection from './components/SourceSelection'
import Post from './components/Post'

export default {
  name: 'App',
  components: {
    SourceSelection,
    Post
  },
  data() {
    return {
      source: 'bbc-news'
    }
  },
  methods: {
    sourceChanged: function (source) {
        this.source = source;
    }
  }
}
</script>

<style lang="scss">
#app {
    font-family: MyliusModernRegular,Helvetica,Arial,sans-serif;
    // -webkit-font-smoothing: antialiased;
    // -moz-osx-font-smoothing: grayscale;
    // text-align: center;
    // color: #2c3e50;
    // margin-top: 60px;
    // padding-top: 20px;
}
</style>
