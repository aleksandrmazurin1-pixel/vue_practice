<template>
  <div class="app">
    <post-form/>
    <post-list :posts="posts"/>

    <div>Привет {{ username }}, у тебя {{ posts.length }} постов</div>
    <div>
      <a v-bind:href="docsLink">{{ linkText }}</a>
    </div>

    <button @click="sayHello">
      Console
    </button>

    <div>
      <p v-if="isLoggedIn === true">Ты вошел в аккаунт</p>
    </div>

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

  </div>
</template>

<script>
import PostForm from "./components/PostForm.vue";
import PostList from "./components/PostList.vue";

export default {
  components: {
    PostForm,
    PostList
  },

  data() {
    return {
      nickname: '',
      posts: [
        {id: 1, title: 'JS', body: 'Description post about JS'},
        {id: 2, title: 'JS2', body: 'Description post about JS2'},
        {id: 3, title: 'JS3', body: 'Description post about JS3'},
        {id: 4, title: 'JS4', body: 'Description post about JS4'}
      ],
      username: 'Alex',
      docsLink: 'https://vuejs.org/guide/introduction.html',
      linkText: 'Открыть доки',
      isLoggedIn: true,
      counter: 0
    }
  },

  methods: {
    incrementCounter() {
      return this.counter++;
    },

    createPost() {
      if (this.title !== '' || this.body !== '') {
        const newPost = {
          id: crypto.randomUUID(),
          title: this.title,
          body: this.body
        }
        this.posts.push(newPost);
        this.title = '';
        this.body = '';
      }
    },

    inputTitle(event) {
      this.title = event.target.value;
    },

    inputBody(event) {
      this.body = event.target.value;
    },
    sayHello() {
      console.log('Привет из sayHello!');
    }
  },

  computed: {
    doubleCounter() {
      return this.counter * 2;
    },
    sortedPosts() {
      
    }
  },

}
</script>

<style>
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

.app {
  padding: 50px;
}
</style>