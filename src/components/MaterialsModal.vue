<template>
  <v-dialog
    v-model="dialogVisible"
    max-width="1000"
    persistent
  >
    <v-skeleton-loader 
      type="card"
      v-if="loading"
    />
    <v-card
      v-if="loaded"
      max-width="1000"
      prepend-icon="mdi-update"
      title="Update in progress"
    >
      <v-card-text>{{ responseHTML }}</v-card-text>
      <template v-slot:actions>
        <v-btn
          class="ms-auto"
          text="Ok"
          @click="closeDialog"
        ></v-btn>
      </template>
    </v-card>
  </v-dialog>
</template>
<script>
  import axios from 'axios'
  export default {
    props: {
      showDialog: {
        type: Boolean,
        required: true
      },
      description: {
        type: String,
        required: true
      },
    },
    data() {
      return {
        dialogVisible: this.showDialog,
        loaded: false,
        loading: false,
        responseHTML: "",
      }
    },
    watch: {
      showDialog: function() {
        this.loading = true
        let url = "https://quotes.toscrape.com/"
        //let url = 'https://www.homedepot.ca/search?q=' + this.description
        this.scrapePage(url)
      }
    },
    methods: {
      closeDialog() {
        this.loading = false
        this.$emit('closeDialog')
      },
      scrapePage(url) {
        axios.get(url)
        .then(response => {
          this.responseHTML = response.data
          console.log(response.data)
        })
        .catch(error => {
          console.error(error);
        }).finally(() => {
          this.loading = false
          this.loaded = true;
        });
      },
    },
  }
</script>