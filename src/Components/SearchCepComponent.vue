<template>
    
    <div class="search-cep">

        <div>

            <h1>Pesquisar CEP</h1>

            <form @submit.prevent="searchCep">

                <label for="cep"></label>

                <input type="text" name="cep" id="cep" v-model="cep">

                <button type="submit">Pesquisar</button>

            </form>

        </div>

        <div>

            <p><b>Cidade: </b>{{address.cidade}}</p>
            <p><b>Estado: </b>{{address.estado}}</p>

        </div>

    </div>

</template>

<style scoped>

    .search-cep {

        width: 50%;
        margin: auto;
        text-align: center;

    }

</style>

<script>
export default {
    data () {

       return {

            cep : "",
            address : {}

       }

    },
    methods : {

        searchCep(){

            this.$http.get("https://api.postmon.com.br/v1/cep/" + this.cep).then(
                response => {
                    console.log(response.body)
                    this.address = response.body
                    
                },
                error => {

                    console.log(error);

                }
            )
        }
    }
}
</script>
