<template>

  <div>
    <NavBar />
    <EditStoreModal :store="selectedStore" />
    <DeleteStoreModal :store="selectedStore" @onDeleted="getAll" />
    <div class="container">
      <h1>
        Stores
        <storeEntryModal class="float-right" @onAdd="getAll" />
      </h1>
      <table class="table table-bordered tabled-striped">
        <thead>
          <tr class="bg-info text-white">
            <th>Brand</th>
            <th>Description</th>
            <th>Product</th>
            <th>Value</th>
            <th>&nbsp;</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="store in stores" :key="store.id">
            <td>{{store.brand}}</td>
            <td>{{store.description}}</td>
            <td>{{store.product}}</td>
            <td>{{store.value}}</td>
            <td>
              <b-button @click="onEdit(store)" variant="info" size="sm">
                Edit
              </b-button>
              <b-button @click="onDelete(store)" variant="danger" size="sm">
                Delete
              </b-button>
            </td>
          </tr>
        </tbody>
      </table>
    </div>

  </div>

</template>

<script>
export default {
  data() {
    return {
      stores: [],
      selectedStore: {}
    }
  },
  methods: {
    async getAll() {
      await this.$axios.get('/api/stores')
      .then((res)=>{
        if(res.status==200){
          this.stores = res.data
        }
      })
    },
    onEdit(selectedStore) {
      this.selectedStore = selectedStore
      this.$bvModal.show('editStoreModal')
    },
    onDelete(selectedStore) {
      this.selectedStore = selectedStore
      this.$bvModal.show('deleteStoreModal')
    }
  },
  created() {
    this.getAll()
  }
}

</script>

<style>

</style>
