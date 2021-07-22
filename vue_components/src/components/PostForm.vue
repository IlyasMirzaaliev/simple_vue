<template>
  <form action="" @submit.prevent>
    <h2>Create Hero</h2>

    <input
        v-model="user.name"
        class="input"
        type="text"
        placeholder="Name">

    <input
        v-model="user.gender"
        class="input"
        type="text"
        placeholder="Last Name">
<!--    <input-->
<!--        type="file"-->
<!--        multiple-->
<!--        class="upload">-->
    <button
        type="button"
        class="btn"
        @click="createPost"
    >Create
    </button>
  </form>
</template>

<script>
export default {
  name: "PostForm",
  data() {
    return {
      user: {
        name: '',
        gender: '',
      }
    }
  },
  methods: {
    createPost() {
      this.user.id = Date.now()
      this.$emit('create',this.user)
      this.user = {
        name: '',
        gender: '',
      }

    }
  }
}
</script>

<style scoped>
form {
  display: flex;
  flex-direction: column;
}

.input {
  width: 100%;
  border: 1px solid teal;
  padding: 10px 15px;
  margin-top: 15px;
}

.btn {
  align-self: flex-end;
  margin-top: 15px;
  padding: 10px 15px;
  background: none;
  color: teal;
  border: 1px solid teal;
}

.upload {
  align-self: start;
  margin-top: 15px;
  padding: 10px 15px;
  background: none;
}
</style>