<template>
    <div>
      <input type="text" v-model="filterText" placeholder="Search...">
    </div>
  </template>
  
  <script>
  export default {
    props: ['items'], // Receive the full list of items
    data() {
      return {
        filterText: '',
      };
    },
    computed: {
      filteredItems() {
        return this.items.filter(item => {
          return item.stock.issue_name.toLowerCase().includes(this.filterText.toLowerCase()); 
        });
      },
    },
    watch: {
      filteredItems() { 
        this.$emit('update-items', this.filteredItems); // Emit updated list
      },
    },
  };
  </script>
  

<style>
input{
    height: 30px;
    width: 500px;
}
</style>
