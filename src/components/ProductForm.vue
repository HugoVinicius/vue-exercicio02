<template>
    <div>
         <b-card bg-variant="dark" text-variant="white" title="Cadastro de Produto"></b-card>
        <div class="container">
      

            <form @submit="onFormRegister" class="form-horizontal">
                <div class="row">
                    <div class="col-25">
                        <label for="name">Nome do Produto: </label>
                        <label>{{name.length}} carac.</label>
                    </div>
                    <div class="col-75">                        
                        <input type="text" placeholder="Informe o nome do produto..." v-model="name">
                        <b-alert show variant="danger" v-if="isNameLimitExceeded">O nome do produto não pode ultrapassar os 15 caracteres</b-alert>        
                    </div>                    
                </div>
                <div class="row">
                    <div class="col-25">
                        <label for="subject">Descrição</label>
                    </div>
                    <div class="col-75">
                        <textarea type="text" v-model="description" placeholder="Informe a descrição do produto..." style="height:100px"></textarea>
                    </div>
                </div>
                <div class="row">
                    <div class="col-25">
                        <label for="lname">Valor do Produto</label>
                    </div>
                    <div class="col-75">
                        <input type="number" step="any" v-model="price" placeholder="Informe o valor do produto Ex.: 10.50">
                    </div>
                </div>
                <div class="row">
                    <input type="submit" value="Cadastrar" class="center">
                </div>
            </form>        
        </div>  
    </div>
</template>

<script>
export default {
    name:"ProductForm",
    props:{
        registerProduct: { 
            type: Function 
        },
    },
    data() {
        return{
            name: "", 
            description: "",
            price: "",  
            error: "",
            isNameLimitExceeded: false
        }
    },
    watch: {
        name: function () {            
            this.isNameLimitExceeded = this.name.length > 15;
        }    
    },
    methods: {
        onFormRegister(event) {
            event.preventDefault();

            if (this.isNameLimitExceeded){
                return;
            }

            let product = {
                      name: this.name,
                      description: this.description,
                      price: this.price,
                      image: {
                        url: "https://picsum.photos/id/180/600/300?image=25",
                        alt: "Sem Imagem",                        
                      }
            };

            this.registerProduct(product);

            this.name = '';
            this.description = '';
            this.price = '';

            event.target.reset();            
        }
    }
}
</script>

<style>
    input[type=submit] {
        display: block;
        margin: 0 auto;
    }

    input[type=text], select, textarea, input[type=number]{
    width: 100%;
    padding: 12px;
    border: 1px solid #ccc;
    border-radius: 4px;
    box-sizing: border-box;
    resize: vertical;
    }

    label {
    padding: 12px 12px 12px 0;
    display: inline-block;
    }

    input[type=submit] {
    background-color: #4CAF50;
    color: white;
    padding: 12px 20px;
    border: none;
    border-radius: 4px;
    cursor: pointer;
    float: right;
    }

    .container {
    border-radius: 5px;
    background-color: #f2f2f2;
    padding: 20px;
    }

    .col-25 {
    float: left;
    width: 25%;
    margin-top: 6px;
    }

    .col-75 {
    float: left;
    width: 75%;
    margin-top: 6px;
    }

    .row:after {
    content: "";
    display: table;
    clear: both;
    }

    .center{
     text-align:center;   
    }

    @media screen and (max-width: 600px) {
    .col-25, .col-75, input[type=submit] {
        width: 100%;
        margin-top: 0;
    }
}
</style>