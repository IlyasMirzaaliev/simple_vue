<template>
  <div class="post">
    <div>
      <div><strong>Post ID:</strong> <strong>{{ user.id }}</strong></div>
      <div><strong>Name:</strong> <strong>{{ user.title }}</strong></div>
      <div><strong>Gender:</strong> <strong>{{ user.body }}</strong></div>
      <!--      <div class="img">-->
      <!--        <img :src="user.image" :alt="user.image">-->
      <!--      </div>-->
    </div>
    <div class="post__btns">
      <my-button
          @click="$router.push(`/posts/${user.id}`)"> <!-- emit-ом передаем выше родителю в PostList -->
        Open
      </my-button>
      <my-button
          @click="$emit('remove', user)"> <!-- emit-ом передаем выше родителю в PostList -->
        Delete
      </my-button>
    </div>
  </div>
</template>

<script>
export default {
  name: "PostItem",
  props: {
    user: {
      type: Object,
      required: true
    }
  },
  // methods: {
  //   removePost() {
  //     this.$emit('remove', this.user)
  //   }
  // }
}
</script>

<style scoped>
.post {
  padding: 15px;
  border: 3px solid teal;
  margin-top: 15px;
  display: flex;
  align-items: center;
  justify-content: space-between;
}


.post__btns {
  display: flex;
  margin-right: 15px;
}
</style>