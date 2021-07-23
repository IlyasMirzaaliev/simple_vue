<template>
  <div class="app">
    <h1>Post List</h1>
    <div class="app__btns">
      <my-button
          @click="showDialog"
      >
        Create Post
      </my-button>
      <my-select
          v-model="selectedSort"
          :options="sortOptions"
      />
    </div>


    <my-dialog v-model:isShowDialog="dialogVisible">
      <post-form
          @create="createPost"
      />
    </my-dialog>


    <post-list
        :posts="sortedPosts"
        @remove="removePost"
        v-if="!isLoading"
    />
    <div v-else>
      <my-loader/>
    </div>


  </div>
</template>


<script>

import PostForm from "@/components/PostForm";
import PostList from "@/components/PostList";
import MyDialog from "@/components/MyDialog";
import MyButton from "@/components/UI/MyButton";
import axios from "axios";
import MyLoader from "@/components/UI/MyLoader";
import MySelect from "@/components/UI/MySelect";


export default {
  components: {MySelect, MyLoader, MyButton, MyDialog, PostList, PostForm},
  data() {
    return {
      posts: [],
      dialogVisible: false,
      isLoading: false,
      selectedSort: '',
      sortOptions: [
        {value: 'name', name: 'By Name'},
        {value: 'gender', name: 'By Gender'}
      ],
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
        this.isLoading = true
        setTimeout(async () => {
          const response = await axios.get('https://rickandmortyapi.com/api/character')
          this.posts = response.data.results
          this.isLoading = false
        }, 1000)

      } catch (e) {
        console.log(e)
      } finally {
        // this.isLoading = false
      }
    }
  },
  mounted() {
    this.fetchPosts()
  },
  computed: {
    sortedPosts() {
      return [...this.posts].sort((arg1, arg2) => {
        return arg1[this.selectedSort]?.localeCompare(arg2[this.selectedSort])
      })
    }
  },
  // watch: {
  //   selectedSort(newValue) {
  //     this.posts.sort((arg1, arg2) => {
  //         return arg1[newValue]?.localeCompare(arg2[newValue])
  //     })
  //   }
  // }

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

.app__btns {
  margin: 12px 0;
  display: flex;
  justify-content: space-between;
}

</style>
