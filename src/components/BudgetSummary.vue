<template>
  <v-row style="height: 100vh">
    <v-col cols="6">
      <FileInputComponent @listMaterials="getListMaterials"/>
    </v-col>
    <v-col cols="6">
      <!-- <button @click="scrapePage('https://www.homedepot.ca/search?q=chair%20white')">Scrapear Página</button> -->
      <button @click="scrapePage('https://quotes.toscrape.com/')">Scrapear Página</button>
      <div v-if="scrapedData">
        <h2>{{ scrapedData.title }}</h2>
        <p>{{ scrapedData.description }}</p>
      </div>
      <ul>
        <li v-for="item in listData" :key="item.id">{{ item }}</li>
      </ul>
    </v-col>
  </v-row>
</template>

<script>
import axios from 'axios'
import FileInputComponent from './FileInput.vue';

export default {
  components:{
    FileInputComponent,
  },
  data() {
    return {
      scrapedData: null,
      listData:[],
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
    },
    getListMaterials(listMaterials) {

      //console.log(listMaterials)
      this.listData = listMaterials
    },
  }
};
</script>