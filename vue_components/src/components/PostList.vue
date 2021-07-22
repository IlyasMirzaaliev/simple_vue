<template>
  <div>
    <h3>User List</h3>
    <post-item
        v-for="user in posts"
        :user="user"
        :key="user.id"
        @remove="$emit('remove', user)" <!-- Передаем выше родителю App --> 
    />
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

</style>
