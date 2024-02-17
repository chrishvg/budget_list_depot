<template>
  <v-card flat>
    <v-card-title class="d-flex align-center pe-2">
      <v-icon icon="mdi-video-input-component"></v-icon> &nbsp;
      List Of Materials

      <v-spacer></v-spacer>

      <v-text-field
        v-model="search"
        prepend-inner-icon="mdi-magnify"
        density="compact"
        label="Search"
        single-line
        flat
        hide-details
        variant="solo-filled"
      ></v-text-field>
    </v-card-title>

    <v-divider></v-divider>

    <v-data-table
      :search="search"
      :headers="headers"
      :items="materials"
      :items-per-page="itemsPerPage"
      :group-by="groupBy"
      item-value="id"
    >
      <template v-slot:group-header="{ item, columns, toggleGroup, isGroupOpen }">
        <tr>
          <td :colspan="columns.length">
            <VBtn
              size="small"
              variant="text"
              :icon="isGroupOpen(item) ? '$expand' : '$next'"
              @click="toggleGroup(item)"
            ></VBtn>
            {{ item.value }}
          </td>
        </tr>
      </template>
      <template v-slot:[`item.actions`]="{ item }">
        <v-icon
          size="small"
          class="me-2"
          @click="selectItem(item)"
        >
          mdi-pencil
        </v-icon>
      </template>
    </v-data-table>
  </v-card>
</template>
  
  <script>
  import { ref } from 'vue';
  
  export default {
    props: {
      materials: {
        type: Array,
        required: false
      }
    },
    data() {
      return {
        search: ref(''),
        itemsPerPage: 12,
        groupBy: [
          { key: 'group', order: 'asc' },
        ],
        headers: [
          { title: 'Description', key: 'description' },
          { title: 'Size', key: 'size' },
          { title: 'Count', key: 'count' },
          { title: 'Units', key: 'unit' },
          { title: 'Actions', key: 'actions', sortable: false },
        ],
      }
    },
    methods: {
      selectItem(item) {
        alert("funciona")
        console.log(item)
      }
    },
  };
  </script>
  