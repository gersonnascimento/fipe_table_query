<template>
  <div id="app">
    <div class="title">
      <h1>{{ title }}</h1>
    </div>

      <ul>
        <li v-for="mark of marks" v-on:click="cars_by_mark(mark.id)">{{ mark }}</li>
      </ul>

  </div>
</template>

<script>
export default {
  name: 'app',
  data () {
    return {
      title: 'Lista de montadoras',
      msg: 'Welcome to Your Vue.js App',
      marks: [],
      cars: []
    }
  },
  methods: {

    cars_by_mark: function(id){
      let promise = this.$http.get('http://fipeapi.appspot.com/api/1/carros/veiculos/'+ id + '.json');
      promise.then(res => res.json()).then(marks => this.marks = marks, err => console.log(err));
    }
  },
  created(){
    let promise = this.$http.get('http://fipeapi.appspot.com/api/1/carros/marcas.json');
    promise.then(res => res.json()).then(marks => this.marks = marks, err => console.log(err));

  }
}
</script>

<style lang="scss">
  .title{
    text-align: center;
  }
</style>
