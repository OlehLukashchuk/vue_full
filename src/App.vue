<template>
  <div class="app">
    <div class="app__btns">
      <my-button class="createNewPost" @click="showModal"
        >Create new post</my-button
      >
      <my-select v-model="selectedSort" :options="sortOptions"></my-select>
    </div>
    <my-dialog v-model:show="dialogVisible">
      <custom-form class="customForm" @createPost="addPost" />
    </my-dialog>
    <custom-list :posts="sortedPosts" @remove="removePost" v-if="!isPostLoading" />
    <h1 v-else>Posts loading...</h1>
  </div>
</template>

<script>
import CustomForm from "@/components/PostForm.vue";
import CustomList from "@/components/PostList.vue";
import axios from "axios";

export default {
  data() {
    return {
      posts: [],
      dialogVisible: false,
      isPostLoading: false,
      selectedSort: "",
      sortOptions: [
        { name: "By title", value: "title" },
        { name: "By description", value: "body" },
      ],
    };
  },
  methods: {
    addPost(newPost) {
      newPost.id = this.posts.length + 1;
      this.posts.push(newPost);
      this.dialogVisible = false;
    },
    removePost(removePost) {
      this.posts = this.posts.filter((post) => post.id !== removePost.id);
    },
    showModal() {
      this.dialogVisible = true;
    },

    async fetchUsers() {
      try {
        this.isPostLoading = true;
        const response = await axios.get(
          "https://jsonplaceholder.typicode.com/posts?_limit=10"
        );
        this.posts = response.data;

        this.isPostLoading = false;
      } catch (error) {
        console.log(error.message);
      }
    },
  },
  components: {
    CustomForm,
    CustomList,
  },
  mounted() {
    this.fetchUsers();
  },
  computed: {
    sortedPosts() {
      return [...this.posts].sort((p1, p2) => {
        return p1[this.selectedSort]?.localeCompare(p2[this.selectedSort]);
      });
    },
  },
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
.app {
  padding: 24px;
}
.customForm {
  margin-bottom: 20px;
}

.createNewPost {
  margin-bottom: 20px;
  font-size: 20px;
  border: none;
}
.app__btns {
  display: flex;
  justify-content: space-between;
}
</style>