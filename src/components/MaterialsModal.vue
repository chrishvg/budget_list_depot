<template>
    <v-dialog
      v-model="dialog"
      width="auto"
    >
      <v-card
        max-width="500"
        prepend-icon="mdi-update"
        text="Your application will relaunch automatically after the update is complete."
        title="Update in progress"
      >
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
  export default {
    props: {
      showDialog: {
        type: Boolean,
        required: true
      }
    },
    data() {
      return {
        dialog: this.showDialog,
      }
    },
    methods: {
      closeDialog() {
        this.$emit('closeDialog')
      },
    },
  }
</script>