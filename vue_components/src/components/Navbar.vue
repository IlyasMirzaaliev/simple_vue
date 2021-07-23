<template>
<div class="navbar">
  <div @click="$router.push('/')">VUE 3 </div>
  <div  class="navbar__btns">
    <my-button @click="$router.push('/posts')">Posts</my-button>
    <my-button  @click="$router.push('/about')" style="margin-left: 20px">About us</my-button>
  </div>
<!--  <router-link to="/posts">Users</router-link>-->
<!--  <router-link to="/about">About</router-link>-->
</div>
</template>

<script>
export default {
  name: "Navbar",
}
</script>

<style scoped>
.navbar {
  height: 50px;
  background-color: lightgray;
  box-shadow: 2px 2px 4px gray;
  display: flex;
}

.navbar__btns {
  margin-left: auto;
}

</style>