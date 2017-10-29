<template>
  <div id="app" class="container">
    <SourceSelection v-on:sourceChanged='sourceChanged'></SourceSelection>
    <NewsList v-bind:src='source'></NewsList>
    <!-- <router-view></router-view> -->
  </div>
</template>

<script>
import SourceSelection from './components/SourceSelection'
import NewsList from './components/NewsList'

export default {
  name: 'app',
  components: {
    SourceSelection,
    NewsList
  },
  data() {
    return {
      source: ''
    }
  },
  methods: {
    sourceChanged(source) {
      this.source = source;  
    }
  }
}
</script>

<style>
#app{
  padding-top: 20px;  
}
</style>
