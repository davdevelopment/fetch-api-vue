<template>
  <div class="App" v-if="!loading && data">
    <div class="App-header">
      <h1>{{data.title}}</h1>
      <time>{{`${data.day}/${data.month}/${data.year}`}}</time>
      <img :src="data.img" :alt=data.alt >
      <p>{{data.alt}}</p>
      <div v-if="loading">
        Cargando...
      </div>
      <div v-if="errored">
        Error {{error}}
      </div>
      <Rating />
    </div>
    
  </div>
</template>

<script>
  import axios from "axios"
  import Rating from "./components/Rating.vue"

  export default {
    name: 'App',
    data(){
      return {
        data: null,
        error: null,
        loading: true,
        errored: false
      }
    },
    mounted() {
      axios
        .get(`https://cors-anywhere.herokuapp.com/https://xkcd.com/${Math.floor(Math.random() * (2529 - 1)) + 1}/info.0.json`)
        .then(response => {
          this.data = response.data
        })
        .catch(error => {
          console.log(error)
          this.errored = true
          this.error = error.message
        })
        .finally(() => this.loading = false)
    },
    components: {
      Rating
    }
  }
</script>

<style lang="scss">
  body {
    margin: 0;
    font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', 'Roboto', 'Oxygen',
      'Ubuntu', 'Cantarell', 'Fira Sans', 'Droid Sans', 'Helvetica Neue',
      sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
  }
  .App {
    text-align: center;
    &-logo {
      height: 40vmin;
      pointer-events: none;
    }
    &-header {
      background-color: #282c34;
      min-height: 100vh;
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      font-size: calc(10px + 2vmin);
      color: white;
    }
    &-link {
      color: #61dafb;
    }
  }
</style>
