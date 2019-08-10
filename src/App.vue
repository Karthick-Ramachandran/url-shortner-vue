<template>
  <div class="row container">
    <div class="col l6 xl6 s12 ">
      <input type="text" @keyup="getData" placeholder="Type your url here (must include https://)">

      <button class="btn" @click="getURL" :disabled="Disabled" >Short</button>
      <h3>Your short url is : <a :href="short"> {{ short }}</a> </h3>

      <p style="color:red"> {{ err }}</p>
    </div>
  </div>
</template>

<script>

import axios from 'axios'

export default {
  name: 'app',
  data() {
    return {
      url: '',
      short: '',
      err : ''
    }
  },
  methods : {
    getData(e) {
      this.url = e.target.value
    },
    getURL() {
      axios.post('https://rel.ink/api/links/', {
        url : this.url
      }).then((response) => {
        this.short = `https://rel.ink/${response.data.hashid}`
      }).catch(err => {
        this.err = "failed to get the data.. make sure you included http://"
      })
    }
  },
  computed: {
    Disabled() {
     return this.url === ''
    }
  }
}
</script>

<style>

</style>
