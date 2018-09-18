<template>
    
    <div class="search-cep">

        <div>

            <h1>Pesquisar CEP</h1>

            <form @submit.prevent="searchCep">

                <label for="cep"></label>

                <input type="text" name="cep" id="cep" v-model="cep">

                <button type="submit" v-if="!loading">Pesquisar</button>

                <button v-if="loading" disabled>Carregando...</button>

            </form>

        </div>

        <div v-if="address.cidade">

            <p><b>Cidade: </b>{{address.cidade}}</p>
            <p><b>Estado: </b>{{address.estado}}</p>

        </div>

        <div v-show="error">
            <p v-text="error"></p>
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
            address : {},
            loading : false,
            error : ""

       }

    },
    methods : {

        searchCep(){
            this.loading = true;
            this.error = "";

            this.$http.get("https://api.postmon.com.br/v1/cep/" + this.cep).then(
                response => {

                    this.address = response.body;
                    
                },
                error => {

                    this.address = {}
                    this.error = "CEP not found"

                }
            ).finally(() => {
                this.loading = false;
            })
        }
    }
}
</script>
