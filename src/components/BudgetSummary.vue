<template>
  <v-row style="height: 100vh">
    <v-col cols="2">
      <FileInputComponent @listMaterials="getListMaterials"/>
    </v-col>
    <v-col cols="10">
      <!-- <button @click="scrapePage('https://www.homedepot.ca/search?q=chair%20white')">Scrapear Página</button> -->
      <button @click="scrapePage('https://quotes.toscrape.com/')">Scrapear Página</button>
      <div v-if="scrapedData">
        <h2>{{ scrapedData.title }}</h2>
        <p>{{ scrapedData.description }}</p>
      </div>
      <ListOfMaterials :materials="listData" @delete="deleteItem"/>
    </v-col>
  </v-row>
</template>

<script>
import axios from 'axios'
import FileInputComponent from './FileInput.vue';
import ListOfMaterials from './ListOfMaterials.vue';

export default {
  components:{
    FileInputComponent,
    ListOfMaterials
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
      this.listData = listMaterials
    },
    deleteItem(id) {
      this.listData = this.listData.filter(item => item.id !== id);
    },
  }
};
</script>