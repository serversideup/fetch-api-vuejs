<style scoped>
    h2{
        text-align: center;
        font-weight: bold;
        font-size: 24px;
    }

    div.example-container{
        display: flex;
        align-items: top;
        width: 75%;
        margin: auto;
    }

    div.fetch-api{
        margin-right: 30px; 
        width: 50%;
    }

    div.axios{
        width: 50%;
    }

    pre{
        text-align: left; 
        padding: 10px; 
        background-color: #EEE; 
        width: 100%; 
        margin: auto; 
        max-width: 400px; 
        max-height: 400px; 
        overflow: scroll; 
        margin-bottom: 20px;
    }
</style>
<template>
    <div style="width: 100%; display: flex; flex-direction: column">
        <h2>GET Requests</h2>
        <div class="example-container">
            <div class="fetch-api">
                <h3>Fetch API</h3>
                <pre>
fetch( 'https://api.roastandbrew.coffee/api/v1/companies' )
    .then( function( response ){
        if( response.status != 200 ){
            throw response.status;
        }else{
            return response.json();
        }
    }.bind(this))
    .then( function( data ){
        this.fetchResponse = data;
    }.bind(this))
    .catch( function( error ){
        this.fetchError = error;
    }.bind(this));
                </pre>
                <pre>{{ fetchResponse }}</pre>
                <button @click="loadFetch()">Load Companies (Fetch)</button>
            </div>
            <div class="axios">
                <h3>Axios</h3>
                <pre>
axios.get(' https://api.roastandbrew.coffee/api/v1/companies' )
    .then( function( response ){
        this.axiosResponse = response.data;
    }.bind(this))
    .catch( function( error ){
        this.axiosError = error;
    }.bind(this));
                </pre>
                <pre>{{ axiosResponse }}</pre>
                <button @click="loadAxios()">Load Companies (Axios)</button>
            </div>
        </div>
    </div>
</template>

<script>
import axios from 'axios';

export default {
    data(){
        return {
            fetchResponse: {},
            fetchError: '',
            axiosResponse: {},
            axiosError: ''
        }
    },

    methods: {
        loadFetch(){
            fetch( 'https://api.roastandbrew.coffee/api/v1/companies' )
                .then( function( response ){
                    if( response.status != 200 ){
                        throw response.status;
                    }else{
                        return response.json();
                    }
                }.bind(this))
                .then( function( data ){
                    this.fetchResponse = data;
                }.bind(this))
                .catch( function( error ){
                    this.fetchError = error;
                }.bind(this));
        },

        loadAxios(){
            axios.get(' https://api.roastandbrew.coffee/api/v1/companies' )
                .then( function( response ){
                    this.axiosResponse = response.data;
                }.bind(this))
                .catch( function( error ){
                    this.axiosError = error;
                }.bind(this));
        }
    }
}
</script>