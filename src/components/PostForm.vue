<template>
  <form class="form1" @submit.prevent>
    <h4>Create new post</h4>
    <my-input
      :data="{
        type: 'text',
        placeholder: 'Enter post title',
      }"
      v-model="postTitle"
    />
    <my-input
      :data="{
        type: 'text',
        placeholder: 'Enter post description',
      }"
      v-model="postDescription"
    />
    <my-button @click="addPost">Create post</my-button>
  </form>
</template>

<script>
export default {
  data() {
    return {
      postTitle: "",
      postDescription: "",
    };
  },
  methods: {
    addPost() {
      let newPost = {
        title: this.postTitle,
        body: this.postDescription,
      };

      this.$emit("createPost", newPost);
      this.postTitle = "";
      this.postDescription = "";
    },
    check() {
    }
  },
};
</script>


<style scoped>
.form1 {
  width: 300px;
  display: flex;
  flex-direction: column;
}
.form1 input {
  margin: 10px 0;
}
</style>