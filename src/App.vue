<template>
  <div id="app">
    <div class="header">
      <div v-if="tab!=0">
        <ul class="header-button-left">
          <li>Cancel</li>
        </ul>
        <ul class="header-button-right">
          <li v-if="tab==1" v-on:click="tab++">Next</li>
          <li v-if="tab==2" v-on:click="post">Submit</li>
        </ul>
      </div>
      <img src="./assets/logo.png" class="logo" />
    </div>

    <Container :postdata="postdata" :tab="tab" :newPost="newPost" @write="newPost.content = $event"/>

    <button v-on:click="more">더보기</button>

    <div class="footer">
      <ul class="footer-button-plus">
        <input type="file" id="file" class="inputfile" v-on:change="upload"/>
        <label for="file" class="input-plus">+</label>
      </ul>
    </div>

    <div></div>
    <div></div>
    <div></div>

  </div>
</template>

<script>

import Container from "@/components/Container"
import postdata from "@/assets/postdata.js"
import axios from "axios";

export default {
  name: 'App',
  data() {
    return {
      tab : 0,
      postdata : postdata,
      inputImg : Object,
      newPost : {
        name: "Kim Hyun",
        userImage: "https://placeimg.com/100/100/arch",
        postImage: "",
        likes: 71,
        date: "April 15",
        liked: false,
        content: "",
        filter: "perpetua"
      },
    }
  },
  components: {
    Container
  },
  methods: {
    post() {
      let postData = this.newPost;

      this.postdata.unshift(postData);
      this.tab = 0;

      this.newPost = {};
    },
    more() {
      axios.get('https://codingapple1.github.io/vue/more1.json')
      .then((result) => {
        this.postdata.push(result.data);
      }).catch((err) => {
        console.log(err);
      });
    },
    upload(e) {
      let files = e.target.files;
      this.$set(this.newPost, 'postImage', URL.createObjectURL(files[0]));

      this.tab = 1;
    }
  }
}

</script>

<style>

  body {
    margin: 0;
  }

  ul {
    padding: 5px;
    list-style-type: none;
  }

  .logo {
    width: 22px;
    margin: auto;
    display: block;
    position: absolute;
    left: 0;
    right: 0;
    top: 13px;
  }

  .header {
    width: 100%;
    height: 40px;
    background-color: white;
    padding-bottom: 8px;
    position: sticky;
    top: 0;
  }

  .header-button-left {
    color: skyblue;
    float: left;
    width: 50px;
    padding-left: 20px;
    cursor: pointer;
    margin-top: 10px;
  }

  .header-button-right {
    color: skyblue;
    float: right;
    width: 50px;
    cursor: pointer;
    margin-top: 10px;
  }

  .footer {
    width: 100%;
    position: sticky;
    bottom: 0;
    padding-bottom: 10px;
    background-color: white;
  }

  .footer-button-plus {
    width: 80px;
    margin: auto;
    text-align: center;
    cursor: pointer;
    font-size: 24px;
    padding-top: 12px;
  }

  .sample-box {
    width: 100%;
    height: 600px;
    background-color: bisque;
  }

  .inputfile {
    display: none;
  }

  .input-plus {
    cursor: pointer;
  }

  #app {
    box-sizing: border-box;
    font-family: "consolas";
    margin-top: 60px;
    width: 100%;
    max-width: 460px;
    margin: auto;
    position: relative;
    border-right: 1px solid #eee;
    border-left: 1px solid #eee;
  }

</style>
