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

    <div>
      <div v-for="post in sortedPosts" :key="post.id">{{ post.title }}</div>
    </div>

    <div v-for="post in posts" :key="post.id">
      <input v-model="post.title">
    </div>

    <div class="inner-mars">
      <b>У тебя {{ shoppingList.length }} постов</b>
    </div>


    <form @submit.prevent>
      <div>

        <input type="text" v-model="newItemName">
        <button @click="addToShoppingList">Добавить задачу</button>

      </div>
    </form>


    <div v-for="list in shoppingList" :key="list.id">
      {{ list.name }}
    </div>


    <form @submit.prevent>
      <div class="inner-mars">
        <input type="text" v-model="targetMovie">
        <button @click="addFavoriteMovie">Добавить фильм</button>
      </div>
    </form>

    <div v-for="movie in favoriteMovies" :key="movie.id">
      {{ movie.name }}
      <button @click="deleteMovie">delete</button>
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
      shoppingList: [
        {id: 1, name: 'Молоко'},
        {id: 2, name: 'Хлеб'},
        {id: 3, name: 'Печенюхи'},
        {id: 4, name: 'Колбаса'},
      ],

      newItemName: '',

      favoriteMovies: [
        {id: 1, name: 'Batman'},
        {id: 2, name: 'Robin'},
        {id: 3, name: 'Joker'},
        {id: 4, name: 'Karl'}
      ],
      movie: '',
      targetMovie: '',

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
    deleteMovie() {
      this.favoriteMovies = this.favoriteMovies.filter(m => m.id === this.movie.id)
    },

    addFavoriteMovie() {
      if (this.targetMovie !== '') {
        const pushMovie = {
          id: crypto.randomUUID(),
          name: this.targetMovie
        }
        this.favoriteMovies.push(pushMovie);
        this.targetMovie = '';
        console.log(this.favoriteMovies);
      }
    },

    incrementCounter() {
      this.counter++;
    },

    addToShoppingList() {
      if (this.newItemName !== '') {
        const newItem = {
          id: crypto.randomUUID(),
          name: this.newItemName,
        }
        this.shoppingList.push(newItem);
        this.newItemName = '';
        console.log(this.shoppingList);
      }
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
      return [...this.posts].sort((a, b) => {
        if (a.title < b.title) return -1;
        if (a.title > b.title) return 1;
        return 0;
      })
    }
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
  padding: 50px;
}

.inner-mars {
  margin-top: 20px;
  background-color: #d3d3d3;
}

</style>