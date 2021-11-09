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

    div.form-container{
        width: 500px;
        text-align: left;
        margin: auto;
        margin-top: 10px;
        margin-bottom: 10px;
    }

    div.form-container label{
        display: block;
    }

    div.form-container input{
        width: 100%;
    }
</style>
<template>
    <div style="width: 100%; display: flex; flex-direction: column">
        <h2>File Upload Requests</h2>

        <div class="form-container">
            <label>Token</label>
            <input type="text" v-model="token"/>
        </div>
        <div class="form-container">
            <label>File</label>
            <input type="file" @change="handleFileUpload( $event )"/>
        </div>

        <div class="example-container">
            <div class="fetch-api">
                <h3>Fetch API</h3>
                <pre>
let formData = new FormData();

formData.append( 'method', this.form.method );
formData.append( 'icon', this.form.icon );

fetch( 'https://api.roastandbrew.coffee/api/v1/brew-methods', {
    method: 'POST',
    headers: {
        'Authorization': 'Bearer '+this.token,
        'Accept': 'application/json',
        'Content-Type': 'multipart/form-data'
    },
    body: formData
} )
.then( function( response ){
    if( response.status != 201 ){
        this.fetchError = response.status;
    }else{
        response.json().then( function( data ){
            this.fetchResponse = data;
        }.bind(this));
    }
}.bind(this));
                </pre>
                <pre>{{ fetchResponse }}</pre>
                <button @click="sendFetch()">Send Data (Fetch)</button>
            </div>
            <div class="axios">
                <h3>Axios</h3>
                <pre>
let formData = new FormData();

formData.append( 'method', this.form.method );
formData.append( 'icon', this.form.icon );

axios.post(' https://api.roastandbrew.coffee/api/v1/brew-methods', 
    formData, {
    headers: {
        'Authorization': 'Bearer '+this.token,
        'Content-Type': 'multipart/form-data'
    }
} )
.then( function( response ){
    this.axiosResponse = response.data;
}.bind(this))
.catch( function( error ){
    this.axiosError = error;
}.bind(this));
                </pre>
                <pre>{{ axiosResponse }}</pre>
                <button @click="sendAxios()">Send Data (Axios)</button>
            </div>
        </div>
    </div>
</template>

<script>
import axios from 'axios';

export default {
    data(){
        return {
            form: {
                method: '',
                icon: ''
            },

            token: '',
            fetchResponse: {},
            fetchError: '',
            axiosResponse: {},
            axiosError: ''
        }
    },

    methods: {
        sendFetch(){
            let formData = new FormData();

            formData.append( 'method', this.form.method );
            formData.append( 'icon', this.form.icon );

            fetch( 'https://api.roastandbrew.coffee/api/v1/brew-methods', {
                method: 'POST',
                headers: {
                    'Authorization': 'Bearer '+this.token,
                    'Accept': 'application/json',
                    'Content-Type': 'multipart/form-data'
                },
                body: formData
            } )
            .then( function( response ){
                if( response.status != 201 ){
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

        sendAxios(){
            let formData = new FormData();

            formData.append( 'method', this.form.method );
            formData.append( 'icon', this.form.icon );

            axios.post(' https://api.roastandbrew.coffee/api/v1/brew-methods', 
                formData, {
                headers: {
                    'Authorization': 'Bearer '+this.token,
                    'Content-Type': 'multipart/form-data'
                }
            } )
            .then( function( response ){
                this.axiosResponse = response.data;
            }.bind(this))
            .catch( function( error ){
                this.axiosError = error;
            }.bind(this));
        },

        handleFileUpload( e ){
            this.form.icon = e.target.files[0];
        }
    }
}
</script>