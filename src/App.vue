<template>
  <div class="header">
    <ul class="header-button-left">
      <li>Cancel</li>
    </ul>
    <ul class="header-button-right">
      <li v-if="tabSelected == 2" @click="publish">발행</li>
      <li v-else @click="tabSelected++">Next</li>
    </ul>
    <img src="./assets/logo.png" class="logo" />
  </div>

  <button
    type="button"
    v-for="(item, idx) in tabs"
    :key="idx" @click="tabSelected = idx"
  >{{ item }}</button>

  <Container
    :postData="postData"
    :tabSelected="tabSelected"
    :imgUrl="imgUrl"
    @newPost="postText = $event" />
  <button type="button" @click="more()">더보기</button>

  <div class="footer">
    <ul class="footer-button-plus">
      <input @change="upload" type="file" id="file" class="inputfile" />
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
      linkNum: 0,
      tabs: ['탭1', '탭2', '탭3'],
      tabSelected: 0,
      imgUrl: '',
      postText: ''
    }
  },
  components: {
    Container,
  },
  methods: {
    more(){
      axios.get(`https://codingapple1.github.io/vue/more${this.linkNum}.json`)
      .then((result) => { //data: GET요청으로 가져온 데이터
        // 요청 성공 시 실행할 코드
        this.postData.push(result.data);
        this.linkNum++;
      })
    },
    upload(event){
      //파일 업로드 시 실행할 코드
      let file = event.target.files; //업로드한 파일 정보
      console.log(file[0]) //파일 정보
      this.imgUrl = URL.createObjectURL(file[0]); //파일 URL 생성
      console.log(this.imgUrl)
      this.tabSelected = 1; //다음 페이지로 이동
    },
    publish(){
      let myPost = {
        name: "Kim Hyun",
        userImage: "https://picsum.photos/100?random=3",
        postImage: "https://picsum.photos/600?random=3",
        likes: 36,
        date: "May 15",
        liked: false,
        content: this.postText,
        filter: "perpetua"
      };
      console.log(this.$emit('newPost').$event)
      this.postData.unshift(myPost); //밀어넣기
      this.tabSelected = 0;
    }
  },
}
</script>

<style>
@import url('./assets/style.css');
</style>
