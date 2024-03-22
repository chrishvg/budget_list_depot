<template>
  <v-row style="height: 100vh">
    <v-col cols="2">
      <FileInputComponent @listMaterials="getListMaterials"/>
    </v-col>
    <v-col cols="10">
      <ListOfMaterials :materials="listData" @delete="deleteItem"/>
    </v-col>
  </v-row>
</template>

<script>
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
    getListMaterials(listMaterials) {
      this.listData = listMaterials
    },
    deleteItem(id) {
      this.listData = this.listData.filter(item => item.id !== id);
    },
  }
};
</script>