<template>
  <div class="app">
      <h1>Post List</h1>
    <my-button
    @click="showDialog"
    style="margin: 12px 0;"
    >
      Create Post
    </my-button>
    <my-dialog v-model:isShowDialog="dialogVisible" >
      <post-form
          @create="createPost"
      />
    </my-dialog>


    <post-list
        :posts="posts"
        @remove="removePost"
    />

  </div>
</template>


<script>

import PostForm from "@/components/PostForm";
import PostList from "@/components/PostList";
import MyDialog from "@/components/MyDialog";
import MyButton from "@/components/UI/MyButton";
import axios from "axios";


export default {
  components: {MyButton, MyDialog, PostList, PostForm},
  data() {
    return {
      posts: [],
      dialogVisible: false
    }
  },

  methods: {
    createPost(user) {
      this.posts.push(user)
      this.dialogVisible = false
    },
    removePost(user) {
      this.posts = this.posts.filter(u => u.id !== user.id)
    },
    showDialog() {
      this.dialogVisible = true
    },
    async fetchPosts() {
      try {
        const response = await axios.get('https://rickandmortyapi.com/api/character')
        this.posts =  response.data.results
      }catch (e) {
        console.log(e)
      }
    }
  },
  mounted() {
    this.fetchPosts()
  },

}


</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
.app {
  padding: 20px;
}

</style>
