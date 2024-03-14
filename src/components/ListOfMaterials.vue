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
   <!-- Modal de confirmación -->
  <v-dialog v-model="mostrarModalEliminar" max-width="500px">
    <v-card>
      <v-card-title class="headline">Confirmation</v-card-title>
      <v-card-text>Are you sure you want to remove this item?</v-card-text>
      <v-card-actions>
        <v-btn
          class="text-none text-subtitle-1"
          color="red"
          size="small"
          variant="elevated"
          @click="eliminar"
        >
          Delete
        </v-btn>
        <v-btn
          class="text-none text-subtitle-1"
          color="grey"
          size="small"
          variant="elevated"
          @click="cerrarModal"
        >
        Cancel
        </v-btn>
      </v-card-actions>
    </v-card>
  </v-dialog>
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
        mostrarModalEliminar: false,
        idEliminar: null,
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
      },
      deleteItem(id) {
        this.idEliminar = id
        this.mostrarModalEliminar = true
      },
      eliminar() {
        this.$emit('delete', this.idEliminar)
        this.cerrarModal()
      },
      cerrarModal() {
        this.mostrarModalEliminar = false
        this.idEliminar = null
      },
    },
  };
  </script>