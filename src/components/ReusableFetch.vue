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
        <h2>Reusable Requests</h2>
        <div class="example-container">
            <div class="fetch-api">
                <h3>Fetch API</h3>
                <pre>{{ brewMethods }}</pre>
                <button @click="loadBrewMethods()">Load Brew Methods (Fetch)</button>
            </div>
            <div>
                <div class="form-container">
                    <label>Name</label>
                    <input type="text" @change="test()" v-model="form.method"/>
                </div>
                <div class="form-container">
                    <label>Icon</label>
                    <input type="file" @change="handleFileUpload( $event )"/>
                </div>
                <button @click="saveBrewMethod()">Save Brew Method (Fetch)</button>
            </div>
        </div>
    </div>
</template>

<script>
import BrewMethodsAPI from '../api/resources/BrewMethods.js';
import { ref } from 'vue';

export default {
    data(){
        return {
            fetchError: '',
            
        }
    },

    setup( ){
        const brewMethods = ref({});
        const loadBrewMethods = async() => {
            brewMethods.value = await BrewMethodsAPI.index();
        };

        const form = {
            method: '',
            icon: ''
        };

        const saveBrewMethod = async() => {
            let formData = new FormData();
            
            formData.append('method', form.method);
            formData.append('icon', form.icon);

            await BrewMethodsAPI.store( formData )
        }

        return {
            brewMethods,
            loadBrewMethods,
            form,
            saveBrewMethod
        }
    },

    methods: {
        handleFileUpload( e ){
            this.form.icon = e.target.files[0];
        }
    }
}
</script>