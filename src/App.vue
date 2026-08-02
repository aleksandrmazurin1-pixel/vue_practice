<template>
  <div class="app">
    <card>
      <p>Это текст из документа «CARD»</p>
    </card>
    <highlight>
      <p>Это просто обычный текст, который я написал прямо здесь, в App.vue</p>
    </highlight>
    <post-form @create-post="addPost"/>
    <div class="block-nine">
      <h4> Фильтр постов</h4>
      <input v-model="searchQuerry">
    </div>
    <div>
      <p>Постов показано сейчас: <span> {{ filteredPosts.length }} </span> </p>
      <p>Постов отмечено избранным: <span> {{ countFavPosts }} </span> </p>
    </div>
    <post-list :posts="filteredPosts" @delete-post="delPost" @change-favorite="changeFavorite"/>
    <button class="btn" @click="ggg">Клик</button>
    <div>
      <p v-if="isLoggedIn">Ты вошел в аккаунт</p>
      <p v-else>Ты yyyttt вошел в аккаунт</p>

    </div>

    <div>Привет {{ username }}, у тебя {{ posts.length }} постов</div>
    <div>
      <a v-bind:href="docsLink">{{ linkText }}</a>
    </div>

    <button @click="sayHello">
      Console
    </button>


    <div> coooo {{ counter }}
      <button @click="incrementCounter">++</button>
    </div>

    <div>
      <input type="text" v-model="nickname">
      <div>{{ nickname }}</div>
    </div>

    <div>
      Счётчик каунтера умножить на два: {{ doubleCounter }}
    </div>

    <div>
      <div v-for="post in sortedPosts" :key="post.id">{{ post.title }}</div>
    </div>

    <div v-for="post in posts" :key="post.id">
      <input v-model="post.title">
    </div>

    <shopping-list/>


    <movie-films :username="username"/>

  </div>
</template>

<script>
import PostForm from "./components/PostForm.vue";
import PostList from "./components/PostList.vue";
import MovieFilms from "@/components/MovieFilms.vue";
import ShoppingList from "./components/ShoppingList.vue";
import Highlight from "@/components/Highlight.vue";
import SlotForm from "@/components/SlotForm.vue";
import Card from "@/components/Card.vue";

export default {
  components: {
    PostForm,
    PostList,
    MovieFilms,
    ShoppingList,
    Highlight,
    SlotForm,
    Card
  },

  data() {
    return {
      nickname: '',
      posts: [
        {id: 1, title: 'JS', body: 'Description post about JS', isFavorite: false},
        {id: 2, title: 'JS2', body: 'Description post about JS2', isFavorite: false},
        {id: 3, title: 'JS3', body: 'Description post about JS3', isFavorite: false},
        {id: 4, title: 'JS4', body: 'Description post about JS4', isFavorite: false}
      ],

      username: 'Alex',
      docsLink: 'https://vuejs.org/guide/introduction.html',
      linkText: 'Открыть доки',
      isLoggedIn: true,
      counter: 0,
      searchQuerry: '',
    }
  },

  methods: {
    ggg() {
      if (this.isLoggedIn) {
      this.isLoggedIn = false;
      } else {
        this.isLoggedIn = true;
      }
    },

    delPost(postId) {
      this.posts = this.posts.filter(post => post.id !== postId);

    },

    changeFavorite(postId) {
      const foundPost = this.posts.find(post => post.id === postId);
      foundPost.isFavorite = !foundPost.isFavorite;
    },

    addPost(post) {
      this.posts.push({id: crypto.randomUUID(), ...post});
    },

    incrementCounter() {
      this.counter++;
    },
    sayHello() {
    }
  },

  computed: {
    countFavPosts() {
      return this.posts.filter(post => post.isFavorite).length;
    },

    doubleCounter() {
      return this.counter * 2;
    },
    sortedPosts() {
      return [...this.posts].sort((a, b) => {
        if (a.title < b.title) return -1;
        if (a.title > b.title) return 1;
        return 0;
      })
    },
    filteredPosts() {
      return this.posts.filter(post => post.title.toLowerCase().includes(this.searchQuerry.toLowerCase()));
    },
  },
  watch: {
    nickname(newVal, oldVal) {
      console.log(newVal, oldVal);
    }
  }

}
</script>

<style>
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

.app {
  background-color: #e1e1e1;
  padding: 50px;
}

.btn {
  background-color: #439019;
  color: #fff;
  font-weight: bold;
  border-radius: 30px;
  padding: 8px 15px;
  border: none;
  margin-top: 10px;
}

.block-nine {
  margin-top: 10px;
  margin-bottom: 10px;
  border: #6e1818 solid 3px;
  box-shadow: #6e1818 0.5px 0.5px 0.5px;
  padding: 10px;
  background-color: #f1e2e2;
}
</style>
