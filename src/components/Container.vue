<template>
  <div>
    <div v-if="tab==0" >
      <Post v-for="(post, i) in postdata" :post="post" :key="i"/>
    </div>

    <div v-else-if="tab==1" >
      <div class="upload-image" :style="{ backgroundImage : `url(${newPost.postImage})`}"></div>
      <div class="filters">
        <div class="filter-1"></div>
        <div class="filter-1"></div>
        <div class="filter-1"></div>
        <div class="filter-1"></div>
        <div class="filter-1"></div>
      </div>
    </div>

    <div v-else-if="tab==2">
      <div class="upload-image" :style="{ backgroundImage : `url(${newPost.postImage})`}"></div>
      <div class="write">
        <textarea class="write-box" v-on:input="$emit('write', $event.target.value)"></textarea>
      </div>
    </div>
  </div>
</template>

<script>

import Post from "./Post.vue";

export default {
  name: "Container",
  components: {
    Post : Post
  },
  props:{
    postdata : Array,
    tab : Number,
    newPost : Object,
  },
}
</script>

<style scoped>
.upload-image {
  width: 100%;
  height: 450px;
  background: cornflowerblue;
  background-size: cover;
}
.filters {
  overflow-x: scroll;
  white-space: nowrap;
}
.filter-1 {
  width: 100px;
  height: 100px;
  background-color: cornflowerblue;
  margin: 10px 10px 10px auto;
  padding: 8px;
  display: inline-block;
  color: white;
  background-size: cover;
}
.filters::-webkit-scrollbar {
  height: 5px;
}
.filters::-webkit-scrollbar-track {
  background: #f1f1f1;
}
.filters::-webkit-scrollbar-thumb {
  background: #888;
  border-radius: 5px;
}
.filters::-webkit-scrollbar-thumb:hover {
  background: #555;
}
.write-box {
  border: none;
  width: 90%;
  height: 100px;
  padding: 15px;
  margin: auto;
  display: block;
  outline: none;
}
</style>