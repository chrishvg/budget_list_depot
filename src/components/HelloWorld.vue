<template>
  <div>
    <button @click="scrapePage('https://quotes.toscrape.com/')">Scrapear Página</button>
    <div v-if="scrapedData">
      <h2>{{ scrapedData.title }}</h2>
      <p>{{ scrapedData.description }}</p>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  data() {
    return {
      scrapedData: null
    };
  },
  methods: {
    scrapePage(url) {
      axios.get(url)
        .then(response => {
          console.log(response.data)
          this.scrapedData = {
            title: "Título extraído",
            description: "Descripción extraída"
          };
        })
        .catch(error => {
          console.error(error);
        });
    }
  }
};
</script>