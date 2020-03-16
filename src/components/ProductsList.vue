<template>
    <div>
        <b-card bg-variant="dark" text-variant="white" title="Lista de Produto"></b-card>
        <div class="row row-list">
            <ProductItem v-for="(product, index) in listProduct" :key="product" :product="product" :index=index :deleteProduct="deleteProduct" ></ProductItem>
        </div>
    </div>
</template>

<script>
import ProductItem from "./ProductItem.vue";

export default {
    name: "ProductsList",
    components: {
        ProductItem,
    },
    props: {
        listProduct:{
            type: Array
        },
        deleteProduct: { 
            type: Function 
        },
    }
}
</script>

<style>
 .row-list {
        margin: 30px !important;
    }
</style>