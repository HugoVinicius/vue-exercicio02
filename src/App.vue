<template>
  <div id="app">
    <!--<img alt="Vue logo" src="./assets/logo.png">-->
    <div class="text-center">
      <h1>
        Quantidade de Produtos: <b-badge variant="light">{{ countListProduct }}</b-badge>
      </h1>
    </div>
    <ProductForm :registerProduct="registerProduct"></ProductForm>
    <ProductList :listProduct="listProduct" :deleteProduct="deleteProduct"/>
  </div>
</template>

<script>
import ProductList from './components/ProductsList.vue'
import ProductForm from './components/ProductForm.vue'

export default {
  name: 'App',
  components: {
    ProductList,
    ProductForm
  },
  data(){
    return{
      listProduct:[]
    }
  },
  mounted () {
    if (localStorage.getItem('listaProduct')) this.listProduct = JSON.parse(localStorage.getItem('listaProduct'));
  },
  computed: {
        countListProduct: function () { 
            return  this.listProduct.length;
        }
  },
  methods: {
    registerProduct(product){
      this.listProduct.push(product);

      localStorage.setItem('listaProduct', JSON.stringify(this.listProduct));
    },
    deleteProduct(index){
      this.listProduct.splice(index, 1);

      localStorage.setItem('listaProduct', JSON.stringify(this.listProduct));
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 0px;
}
</style>
