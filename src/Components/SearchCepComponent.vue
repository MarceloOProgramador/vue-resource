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
            loading : false

       }

    },
    methods : {

        searchCep(){
            this.loading = true;

            this.$http.get("https://api.postmon.com.br/v1/cep/" + this.cep).then(
                response => {

                    this.address = response.body;
                    
                },
                error => {

                    console.log(error);

                }
            ).finally(() => {
                this.loading = false;
            })
        }
    }
}
</script>
