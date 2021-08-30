<template>
  <div id="app">
    <div
      @click="toggle(index)"
      class=""
      v-for="(post, index) in limitFive"
      :key="post.id"
    >
      <div class="wrap-title">
        <div class="title">{{ post.title }} {{ index }}</div>
        <div v-show="id === index">{{ post.body }}</div>
      </div>
    </div>
    <div v-if="isLoading">
      <div class="lds-dual-ring"><div></div></div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "App",
  data: () => ({
    posts: [],
    id: "",
    isLoading: "false",
  }),
  components: {},
  mounted() {
    const getData = async () => {
      this.isLoading = true;
      const res = await axios.get("https://jsonplaceholder.typicode.com/posts");
      this.posts = res.data;
      this.isLoading = false;
    };
    getData();
  },
  computed: {
    limitFive() {
      return this.posts.filter((post, index) => index < 3);
    },
  },
  methods: {
    toggle(i) {
      if (this.id === "") {
        this.id = i;
      } else {
        if (i !== this.id) {
          this.id = i;
        } else {
          this.id = "";
        }
      }
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.wrap-title {
  background-color: rgb(106, 209, 175);
  padding: 20px;
  margin: 10px;
  cursor: pointer;
}

.title {
  font-weight: 700;
  font-size: 25px;
}

.lds-dual-ring {
  display: inline-block;
  width: 80px;
  height: 80px;
}
.lds-dual-ring:after {
  content: " ";
  display: block;
  width: 64px;
  height: 64px;
  margin: 8px;
  border-radius: 50%;
  border: 6px solid #fff;
  border-color: rgb(29, 176, 202) transparent rgb(29, 176, 202) transparent;
  animation: lds-dual-ring 1.2s linear infinite;
}
@keyframes lds-dual-ring {
  0% {
    transform: rotate(0deg);
  }
  100% {
    transform: rotate(360deg);
  }
}
</style>
