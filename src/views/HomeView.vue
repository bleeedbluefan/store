<!-- 'view' for HOME PAGE: search box, retrieves product list from global data structure,
      uses 'ProductList' component to display list of all products. -->

<template> 
  <div>
    <div class="wrapper">
      <div class="search">
        <form class="pure-form">
          <i class="fas fa-search"></i><input v-model="searchText" />
        </form>
      </div>
    </div>      <!--\/ \/  is the 'props' from ProductList-->
    <ProductList :products="productss" />
           <!--  /\ /\ /\ is a 'computed'-->
    <div class='bottom-container'>
      <div class='source'> <a href='https://github.com/BYUCS260/grocery-store-bleeedbluefan'>Source</a></div>
    </div>
  </div>        
       
  
</template>

<script>
// We add ProductList to the export as it's now a part of the code
import ProductList from "../components/ProductList.vue"
export default {
  name: 'HomeView',
  components: {
    // Passed all data from 'ProductList.vue'
    ProductList
  },
  data() {
    return {
      searchText: '',
    }

  },
  computed: {
    // Used above to gain the list of products from ProductList
    productss() {
      return this.$root.$data.products.filter(product => product.name.toLowerCase().search(this.searchText.toLowerCase()) >= 0);
    }
  },
}
</script>


<style scoped>
.wrapper {
  display: flex;
  align-items: center;
  justify-content: center;
}

.search {
  border: 1px solid #ccc;
  border-radius: 4px;
  width: 50%;
}

form {
  display: table;
  width: 100%;
}

i {
  display: table-cell;
  padding-left: 10px;
  width: 1px;
}

input {
  display: table-cell;
  font-size: 20px;
  border: none !important;
  box-shadow: none !important;
  width: 100%;
  height: 40px;
}

.bottom-container {
    position: fixed;
    bottom: 0;
    width: 100%;
    padding: 10px;
    background-color: white;
    border: 1px solid black;
}
</style>

