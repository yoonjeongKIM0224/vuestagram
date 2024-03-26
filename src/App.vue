<template>
  <div class="header">
    <ul class="header-button-left">
      <li>Cancel</li>
    </ul>
    <ul class="header-button-right">
      <li>Next</li>
    </ul>
    <img src="./assets/logo.png" class="logo" />
  </div>

  <Container :postData="postData" />
  <button type="button" @click="btnNum++, more()">더보기</button>

  {{ btnNum }}

  <div class="footer">
    <ul class="footer-button-plus">
      <input type="file" id="file" class="inputfile" />
      <label for="file" class="input-plus">+</label>
    </ul>
 </div>
</template>

<script>
import Container from './components/TheContainer.vue';
import PostData from './assets/postData.js';
import axios from 'axios';

export default {
  name: 'App',
  data(){
    return {
      postData: PostData,
      btnNum: 0,
    }
  },
  components: {
    Container,
  },
  methods: {
    more(){
      let link = '';

      if(this.btnNum === 1){
        link = 'https://codingapple1.github.io/vue/more0.json';
      } else if (this.btnNum === 2) {
        link = 'https://codingapple1.github.io/vue/more1.json';
      }

      axios.get(link)
      .then((result) => { //data: GET요청으로 가져온 데이터
        // 요청 성공 시 실행할 코드
        this.postData.push(result.data);
      })
    }
  },
}
</script>

<style>
@import url('./assets/style.css');
</style>
