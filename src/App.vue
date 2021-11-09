<template>
  <img alt="Vue logo" src="./assets/logo.png">

  <get-requests/>
  <post-put-patch-requests/>
  <file-uploads/>
  <reusable-fetch/>
</template>

<script>
import GetRequests from './components/GetRequests.vue';
import PostPutPatchRequests from './components/PostPutPatchRequests.vue';
import FileUploads from './components/FileUploads.vue';
import ReusableFetch from './components/ReusableFetch.vue';

export default {
  name: 'App',
  components: {
    GetRequests,
    PostPutPatchRequests,
    FileUploads,
    ReusableFetch
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
  margin-top: 60px;
}
</style>
