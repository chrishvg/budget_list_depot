<template>
  <v-card flat>
    <v-card-title class="d-flex">
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
          class="me-2"
          @click="selectItem(item)"
        >
          mdi-pencil
        </v-icon>
        <v-icon
          class="me-2"
          @click="deleteItem(item.id)"
        >
          mdi-close	
        </v-icon>
      </template>
    </v-data-table>
  </v-card>
  <ConfirModal v-model="showModalDelete" 
    @confirmDelete="confirmDelete" 
    @closeDialog="closeConfirmModal" 
  />
  <MaterialsModal v-model="showModalMaterials" @closeDialog="closeMaterialsModal"/>
</template>
  
<script>
  import { ref } from 'vue';
  import ConfirModal from './ConfirModal';
  import MaterialsModal from "./MaterialsModal";
  
  export default {
    components: {
      ConfirModal,
      MaterialsModal,
    },
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
        showModalDelete: false,
        showModalMaterials: false,
        idDelete: null,
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
        this.showModalMaterials = true
        console.log(item)
      },
      deleteItem(id) {
        this.idDelete = id
        this.showModalDelete = true
      },
      confirmDelete() {
        this.$emit('delete', this.idDelete)
        this.closeConfirmModal()
      },
      closeConfirmModal() {
        this.showModalDelete = false
        this.idDelete = null
      },
      closeMaterialsModal() {
        this.showModalMaterials = false
      }
    },
  };
  </script>