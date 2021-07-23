<template>
  <div>
    <b-button v-b-modal.storeEntryModal variant="primary">Add Store</b-button>
    <b-modal id="storeEntryModal" title="Store Entry" ok-title="Save Store" @ok="onSubmit">
      <form action="#">
        <b-form-group
          label="Brand"
          label-for="brand"
        >
          <b-form-input id="brand" v-model="store.brand" trim></b-form-input>
        </b-form-group>

        <b-form-group
          label="Description"
          label-for="description"
        >
          <b-form-input id="description" v-model="store.description" trim></b-form-input>
        </b-form-group>

        <b-form-group
          label="Product"
          label-for="product"
        >
          <b-form-input id="product" v-model="store.product" trim></b-form-input>
        </b-form-group>

        <b-form-group
          label="Value "
          label-for="value"
        >
          <b-form-input id="value" v-model="store.value" trim></b-form-input>
        </b-form-group>

        

      </form>
    </b-modal>
  </div>
</template>

<script>
export default {
  data() {
    return {
      store: {},
      
    }
  },
  methods: {
    async onSubmit() {
      this.$axios.post('/api/stores', this.store)
      .then((res)=>{
        if(res.status==202) {
          alert('Successfully added the store')
          this.$emit('onAdd')
        }
      });
    }
  }
}
</script>
