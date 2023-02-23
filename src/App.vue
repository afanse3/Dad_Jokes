<template>
  <body>
    <div class="container">
      <h1>Dad Jokes</h1>
    </div>
    <div class="card">
      <div class="wrapper" v-if="joke">
        <h3>{{ joke.setup }}</h3>
        <br />
        <p>{{ joke.punchline }}</p>
        <p>&#128514;</p>
        <br />
        <button @click="reloadPage">Reload &#128171;</button>
      </div>
      <div class="wrapper" v-else>
        <p>Loading...</p>
      </div>
    </div>
  </body>
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      joke: null,
    };
  },
  mounted() {
    axios.get('https://official-joke-api.appspot.com/random_joke')
    .then(response => {
      this.joke = response.data;
    })
    .catch(error => {
      console.log(error);
    })
  },
  methods: {
    reloadPage() {
      window.location.reload();
    }
  }
}
</script>

<style>
.container {
  margin: 0 auto;
  margin-top: 20px;
  text-align: center;
}

@media (max-width: 768px) {
  .container {
    max-width: 90%;
    padding: 10px;
  }
}

body {
  justify-content: center;
  align-items: center;
  margin: 0;
}

.card {
  margin-top: 20px;
  padding: 20px;
  text-align: right;
  color: black;
}

.card:hover {
  box-shadow: 0 8px 16px 0 rgba(0,0,0,0.2);
}

.wrapper {
  padding: 20px;
  border-radius: 5px;
  background-color: white;
}

.wrapper p {
  font-weight: bold;
}

button {
  padding: 10px 25px;
  font-size: 16px;
  border-radius: 5px;
  border: none;
  background-color: black;
  color: #fff;
  cursor: pointer;
}



</style>
