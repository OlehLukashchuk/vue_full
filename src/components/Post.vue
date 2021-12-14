<template>
  <div class="post">
    <div class="postInfo">
      <div><strong>Title</strong>: {{ post.title }}</div>
      <div><strong>Description</strong>: {{ post.body }}</div>
    </div>
    <div class="postButtons">
      <my-button class="btn deletePost" @click="removePost"
        >Delete Post</my-button
      >
      <my-button class="btn editPost">Edit Post</my-button>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    post: {
      type: Object,
      required: true,
    },
  },
  methods: {
    removePost() {
      this.$emit("remove", this.post);
    },
  },
};
</script>

<style scoped>
.post {
  padding: 15px;
  border: 3px solid teal;
  margin-top: 10px;
  display: flex;
  justify-content: space-between;
  align-items: center;
}
.postInfo {
  width: 90%;
}
.postButtons {
  display: flex;
  flex-direction: column;
}

.postButtons button {
  margin: 5px 0 0;
}
</style>