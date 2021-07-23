<template>
  <div v-if="posts.length > 0">
    <h3>User List</h3>
    <transition-group name="post">
      <post-item
          v-for="user in posts"
          :user="user"
          :key="user.id"
          @remove="$emit('remove', user)" /><!-- Передаем выше родителю App -->
    </transition-group>


  </div>
    <div v-else style="color: red">
      <h2 >List Empty</h2>
    </div>
</template>

<script>
import PostItem from "@/components/PostItem";

export default {
  name: "PostList",
  components: {PostItem},
  props: {
    posts: {
      type: Array,
      required: true
    }
  },
}
</script>

<style scoped>
.post-item {
  display: inline-block;
  margin-right: 10px;
}
.post-enter-active,
.post-active {
  transition: all 0.4s ease;
}
.post-enter-from,
.post-leave-to {
  opacity: 0;
  transform: translateY(130px);
}
</style>
