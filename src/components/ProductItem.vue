<template>
        <div class="col-sm-12 col-md-3">
        <b-card
            v-bind:title="product.name"
            v-bind:img-src="product.image.url"   
            v-bind:img-alt="product.image.alt"
            img-top
            tag="article"
            style="max-width: 20rem;"
            class="mb-2"
        >
            <b-card-text><strong>Descrição: </strong> {{product.description}}</b-card-text>
            <b-card-text><strong>Valor: </strong> {{product.price}}</b-card-text>
            <b-button href="#" variant="btn btn-xs btn-danger" @click="deleteProduct(index)">Excluir</b-button>
        </b-card>  
        </div>
</template>
<script>
export default {
    name:"ProductItem",
    props: {
        product: {
            Type: Object
        },
        index: {
            Type: String/Number
        },
        deleteProduct: { 
            Type: Function 
        }
    },
}

</script>

<style>
    .item{
        background: #dddddd;   
    }
</style>