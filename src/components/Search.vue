<template>
    <div>
      <input type="text" v-model="filterText" placeholder="Search...">
    </div>
  </template>
  
  <script>
  export default {
    props: ['items'], 
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
        this.$emit('update-items', this.filteredItems); 
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
