<template>
  <div class="postsContainer" v-if="posts.length > 0">
    <h3>Posts list</h3>
    <transition-group name="post-list">
      <Post
        v-for="post in posts"
        :key="post.id"
        :post="post"
        @remove="$emit('remove', post)"
      />
    </transition-group>
  </div>
  <h3 v-else class="emptyList">Posts list empty</h3>
</template>

<script>
import Post from "@/components/Post.vue";

export default {
  props: {
    posts: {
      type: Array,
      required: true,
    },
  },
  components: {
    Post,
  },
};
</script>

<style scoped>
.postsContainer {
  display: flex;
  flex-direction: column;
}
.emptyList {
  color: red;
}
.post-list-item {
  display: inline-block;
  margin-right: 10px;
}
.post-list-enter-active,
.post-list-leave-active {
  transition: all 0.5s ease;
}
.post-list-enter-from,
.post-list-leave-to {
  opacity: 0;
  transform: translateX(30px);
}
.post-list-move {
  transition: transform 0.5s ease;
}
</style>