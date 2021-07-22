<template>
  <div class="app">
      <h1>Post List</h1>
    <my-button
    @click="showDialog"
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
// const user =
//     {
//       "id": 1,
//       "name": "Rick Sanchez",
//       "status": "Alive",
//       "species": "Human",
//       "type": "",
//       "gender": "Male",
//       "image": "https://rickandmortyapi.com/api/character/avatar/1.jpeg",
//     }


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
    },
    removePost(user) {
      this.posts = this.posts.filter(u => u.id !== user.id)
    },
    showDialog() {
      this.dialogVisible = true
    }
  }
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
