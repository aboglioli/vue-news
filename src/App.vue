<template>
  <div class="container" id="app">

    <SourceSelection apiKey="apiKey" v-on:sourceChanged="sourceChanged"></SourceSelection>
    <NewsList apiKey="apiKey" v-bind:source="source"></NewsList>

    <footer>alan.boglioli@gmail.com</footer>
  </div>
</template>

<script>
import SourceSelection from './components/SourceSelection';
import NewsList from './components/NewsList';

export default {
  name: 'app',
  components: {
    SourceSelection,
    NewsList
  },
  data() {
    return {
      source: '',
      apiKey: '<YOUR-API-KEY>' // Replace with your API KEY obtained from newsapi.org
    };
  },
  methods: {
    sourceChanged(source) {
      this.source = source;
    }
  }
}
</script>

<style>
#app {
  padding-top: 20px;
}

footer {
  margin-top: 20px;
  background-color: #eee;
  padding: 10px;
  text-align: center;
  border-radius: 3px;
  font-weight: bold;
}
</style>
