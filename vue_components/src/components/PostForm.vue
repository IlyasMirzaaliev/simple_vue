<template>
  <form action="" @submit.prevent>
    <h2>Create Hero</h2>

    <my-input
        v-model="user.title"
        type="text"
        placeholder="Name"/>

    <my-input
        v-model="user.body"
        type="text"
        placeholder="Gender"/>
    <!--    <input-->
    <!--        type="file"-->
    <!--        multiple-->
    <!--        class="upload">-->
    <my-button
        type="button"
        style="align-self: flex-end; margin-top: 15px"
        @click="createPost"
    >Create
    </my-button>
  </form>
</template>

<script>
export default {
  name: "PostForm",
  data() {
    return {
      user: {
        title: '',
        body: '',
      }
    }
  },
  methods: {
    createPost() {
      this.user.id = Date.now()
      this.$emit('create', this.user) //<!-- Передаем родителю выше App.vue -->
      this.user = {
        title: '',
        body: '',
      }
    }
  },
}
</script>

<style scoped>
form {
  display: flex;
  flex-direction: column;
}


.upload {
  align-self: start;
  margin-top: 15px;
  padding: 10px 15px;
  background: none;
}
</style>