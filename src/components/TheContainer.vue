<template>
    <div>
        <Post 
        v-for="(item, idx) in postData"
        :key="idx"
        :item="item" />
    </div>
  </template>
  
  <script>
  import Post from './ThePost.vue';
  
  export default {
    name: 'TheContaienr',
    props: {
        postData: Array
    },
    components: {
        Post,
    }
  }
  </script>
  