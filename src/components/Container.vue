<template>
  <div>
    <Post v-for="(post, i) in postdata" :post="post" :key="i"/>
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
  },
}
</script>

<style scoped>

</style>