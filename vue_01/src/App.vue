<template>
  <div class="app">
    <form action="" @submit.prevent>
      <h2>Create Hero</h2>

      <input
          v-model="name"
          class="input"
          type="text"
          placeholder="Name">

      <!-- двухсторонняя свзяь через $event.target.value -->
      <input
          :value="gender"
          @input="gender = $event.target.value"
          class="input"
          type="text"
          placeholder="Last Name">
      <input
          type="file"
          multiple
          class="upload">
      <button
          type="button"
          class="btn"
          @click="createPost"
      >Create
      </button>
    </form>


    <div class="post" v-for="user in posts" :key="user.id">
      <div><strong>Name:</strong> <strong>{{ user.name }}</strong></div>
      <div><strong>Gender:</strong> <strong>{{ user.gender }}</strong></div>
      <div class="img">
        <img :src="user.image" :alt="user.image">
      </div>
    </div>
  </div>
</template>


<script>

const user =
    {
      "id": 1,
      "name": "Rick Sanchez",
      "status": "Alive",
      "species": "Human",
      "type": "",
      "gender": "Male",
      "image": "https://rickandmortyapi.com/api/character/avatar/1.jpeg",
    }


export default {
  data() {
    return {
      posts: [
        user,
      ],
      name: '',
      gender: ''
    }
  },
  methods: {
    createPost() {
      const newPost = {
        id: Date.now(),
        name: this.name,
        gender: this.gender
      }
      this.posts.push(newPost)
      this.name = ''
      this.gender = ''
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

.post {
  padding: 15px;
  border: 3px solid teal;
  /*color: rgba(34, 12, 64, 0.6);*/
  margin-top: 15px;
}

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

/*#nav {*/
/*  padding: 30px;*/
/*}*/

/*#nav a {*/
/*  font-weight: bold;*/
/*  color: #2c3e50;*/
/*}*/

/*#nav a.router-link-exact-active {*/
/*  color: #42b983;*/
/*}*/
</style>
