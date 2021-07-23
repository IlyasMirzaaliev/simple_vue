<template>
  <div >
    <h1>Post List</h1>
    <my-input
        v-model="searchQuery"
    />
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
        :posts="sortedAndSearchedPosts"
        @remove="removePost"
        v-if="!isLoading"
    />
    <div v-else>
      <my-loader/>
    </div>
    <div class="observer" ref="observer"></div>

    <!--    <div class="page__wrapper">-->
    <!--      <div-->
    <!--          v-for="pageNumber in totalPage"-->
    <!--          :key="pageNumber"-->
    <!--          class="page"-->
    <!--          :class="{-->
    <!--            'current-page': page === pageNumber-->
    <!--          }"-->
    <!--          @click="changePage(pageNumber)"-->
    <!--      >-->
    <!--        {{ pageNumber }}-->
    <!--      </div>-->
    <!--    </div>-->

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
import MyInput from "@/components/UI/MyInput";


export default {
  components: {MyInput, MySelect, MyLoader, MyButton, MyDialog, PostList, PostForm},
  data() {
    return {
      posts: [],
      dialogVisible: false,
      isLoading: false,
      selectedSort: '',
      searchQuery: '',
      page: 1,
      limit: 10,
      totalPage: 0,
      sortOptions: [
        {value: 'title', name: 'By Title'},
        {value: 'body', name: 'By Body'}
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
          const response = await axios.get('https://jsonplaceholder.typicode.com/posts?_limit=10', {
            params: {
              _page: this.page,
              _limit: this.limit
            }
          });
          this.totalPage = Math.ceil(response.headers ['x-total-count'] / this.limit)
          this.posts = response.data
          this.isLoading = false
        }, 1000)

      } catch (e) {
        console.log(e)
      } finally {
        // this.isLoading = false
      }
    },
    async loadPost() {
      try {
        this.page += 1
        // this.isLoading = true
        setTimeout(async () => {
          const response = await axios.get('https://jsonplaceholder.typicode.com/posts?_limit=10', {
            params: {
              _page: this.page,
              _limit: this.limit
            }
          });
          this.totalPage = Math.ceil(response.headers ['x-total-count'] / this.limit)
          this.posts = [...this.posts, ...response.data]
          this.isLoading = false
        }, 1000)

      } catch (e) {
        console.log(e)
      } finally {
        // this.isLoading = false
      }
    },
    // changePage(pageNumber) {
    //   this.page = pageNumber
    //   this.fetchPosts()
    // }
  },
  mounted() {
    this.fetchPosts()
    const options = {
      rootMargin: "0px",
      threshold: 1.0
    }
    const callBack = (entries, observer) => {
      if(entries[0].isIntersecting && this.page.length < this.totalPage) {
        this.loadPost()
      }
    }
    const observer = new IntersectionObserver(callBack, options)
    observer.observe(this.$refs.observer)
  },
  computed: {
    sortedPosts() {
      return [...this.posts].sort((arg1, arg2) => {
        return arg1[this.selectedSort]?.localeCompare(arg2[this.selectedSort])
      })
    },
    sortedAndSearchedPosts() {
      return this.sortedPosts.filter(user => user.title.toLowerCase().includes(this.searchQuery.toLowerCase()))
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


.app__btns {
  margin: 12px 0;
  display: flex;
  justify-content: space-between;
}

.page__wrapper {
  display: flex;
  margin-top: 15px;

}

.page {
  align-self: end;
  border: 1px solid black;
  padding: 10px;


}

.current-page {
  border: 2px solid teal;
}

/*.observer {*/
/*  height: 30px;*/
/*  background: green;*/
/*}*/

</style>
