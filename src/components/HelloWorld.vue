<template>
  <v-row style="height: 100vh">
    <v-col cols="6">
      <v-file-input
        v-model="files"
        color="deep-purple-accent-4"
        counter
        label="File input"
        placeholder="Select your file"
        prepend-icon="mdi-paperclip"
        variant="outlined"
        style="height: 100vh"
      >
        <template v-slot:selection="{ fileNames }">
          <template v-for="(fileName) in fileNames" :key="fileName">
            <v-chip
              color="deep-purple-accent-4"
              label
              size="small"
              class="me-2"
            >
              {{ fileName }}
            </v-chip>
          </template>
        </template>
      </v-file-input>
    </v-col>
    <v-col cols="6">
      <button @click="scrapePage('https://quotes.toscrape.com/')">Scrapear Página</button>
      <div v-if="scrapedData">
        <h2>{{ scrapedData.title }}</h2>
        <p>{{ scrapedData.description }}</p>
      </div>
    </v-col>
  </v-row>
</template>

<script>
import axios from 'axios'

export default {
  data() {
    return {
      scrapedData: null,
      files: [],
    };
  },

  watch: {
    files: function(oldVal, newVal) {
      console.log(oldVal)
      console.log(newVal)
    }
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