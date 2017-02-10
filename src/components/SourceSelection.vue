<template>
  <div class="source-selection">
    <div class="jumbotron">
      <h2>
        <span class="glyphicon glyphicon-list-alt"></span>
        News List
      </h2>
      <h4>Select News source</h4>

      <select class="form-control" v-on:change="sourceChanged">
        <option v-bind:value="source.id" v-for="source in sources">{{source.name}}</option>
      </select>

      <div v-if="source">
        <h6>{{source.description}}</h6>
        <a v-bind:href="source.url" class="btn btn-primary" target="_blank">Go to {{source.name}} website</a>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'source-selection',
  props: ['apiKey'],
  data() {
    return {
      sources: [],
      source: ''
    };
  },
  methods: {
    sourceChanged(e) {
      this.sources.some(s => {
        if(s.id === e.target.value) {
          this.source = s;
          return true;
        }
        return false;
      });
      this.$emit('sourceChanged', this.source);
    }
  },
  created() {
    this.$http
      .get(`https://newsapi.org/v1/sources?language=en&apiKey=${this.apiKey}`)
      .then(res => this.sources = res.data.sources);
  }
}
</script>

<style scoped>
</style>
