<template>
  <div class="post">
    <div>
      <div><strong>Name:</strong> <strong>{{ user.name }}</strong></div>
      <div><strong>Gender:</strong> <strong>{{ user.gender }}</strong></div>
      <div class="img">
        <img :src="user.image" :alt="user.image">
      </div>
    </div>
      <div >
        <my-button>Delete</my-button>
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
  }
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


.user__btns{

}
</style>