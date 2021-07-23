<template>
  <div>

    <b-modal id="deleteStoreModal" title="Store Entry" ok-title="Delete Store" @ok="onDelete" ok-variant="danger">
      Are you sure about deleting this store? <br>
      {{ store.brand }} {{ store.description }}
    </b-modal>
  </div>
</template>

<script>
export default {
  props: {
    store: {}
  },
  methods: {
    async onDelete() {
      this.$axios.delete('/api/stores/' + this.store.id)
      .then((res)=>{
        if(res.status==202) {
          alert('Store is deleted successfully!')
          this.$emit('onDeleted')
        }
      })
    }
  }
}
</script>
