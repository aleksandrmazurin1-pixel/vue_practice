<template>
  <!-- Корневой элемент шаблона. Vue 3 разрешает несколько корней, но тут используется один <div> -->
  <div class="app">
    <!-- <post-form/> — использование дочернего компонента PostForm.
         kebab-case (post-form) в шаблоне соответствует PascalCase (PostForm) в JS-коде ниже.
         Самозакрывающийся тег /> — аналог <img/> в обычном HTML -->
    <post-form/>

    <!-- <post-list :posts="posts"/> — использование компонента PostList
         с передачей пропа (аргумента) "posts".
         ":posts" — сокращение (shorthand) от "v-bind:posts".
         Слева "posts" — имя пропа внутри PostList, справа "posts" — переменная из data() этого компонента.
         Аналогия в чистом JS: postList(posts) — передача аргумента в функцию -->
    <post-list :posts="posts"/>

    <div>Привет {{ username }}, у тебя {{ posts.length }} постов</div>
    <div>
      <a v-bind:href="docsLink">{{ linkText }}</a>
    </div>

    <button @click="sayHello">
      Console
    </button>

  </div>
</template>

<script>
// import — обычный ES6-импорт, ничего специфичного для Vue.
// Указываем путь до файла компонента и полное расширение .vue
import PostForm from "./components/PostForm.vue";
import PostList from "./components/PostList.vue";

export default {
  // components — объект-реестр: "какие дочерние компоненты можно использовать в <template> этого файла".
  // Запись { PostForm, PostList } — ES6-сокращение (property shorthand) для { PostForm: PostForm, PostList: PostList }
  components: {
    PostForm,
    PostList
  },

  // data() — функция (обязательно функция, не объект!), возвращающая объект
  // с реактивным состоянием компонента. Каждое поле здесь Vue "оборачивает"
  // в реактивность (через Proxy), чтобы отслеживать изменения и обновлять DOM автоматически.
  data() {
    return {
      // Массив объектов-постов. Именно его мы передаём в PostList через :posts="posts"
      posts: [
        {id: 1, title: 'JS', body: 'Description post about JS'},
        {id: 2, title: 'JS2', body: 'Description post about JS2'},
        {id: 3, title: 'JS3', body: 'Description post about JS3'},
        {id: 4, title: 'JS4', body: 'Description post about JS4'}
      ],
      username: 'Alex',
      docsLink: 'https://vuejs.org/guide/introduction.html',
      linkText: 'Открыть доки'
    }
  },

  // methods — объект с функциями-обработчиками. Внутри них "this" указывает
  // на сам компонент (точнее, на его реактивный экземпляр), поэтому this.posts,
  // this.title и т.д. — это доступ к полям из data() выше.
  methods: {
    // ⚠️ Этот метод сейчас нигде не вызывается в шаблоне (в App.vue больше нет формы)
    createPost() {
      // Проверка: если хотя бы одно из полей не пустое — создаём пост
      // (условие на "||" здесь спорное: сработает, даже если заполнено только одно поле)
      if (this.title !== '' || this.body !== '') {
        const newPost = {
          // crypto.randomUUID() — не Vue, а обычный Web API браузера,
          // генерирует случайный уникальный идентификатор (строку)
          id: crypto.randomUUID(),
          title: this.title,
          body: this.body
        }
        // .push() — обычный метод массива из чистого JS.
        // Vue отследит это изменение и автоматически перерисует список в PostList
        this.posts.push(newPost);
        // Очищаем поля формы после добавления
        this.title = '';
        this.body = '';
      }
    },

    // ⚠️ Тоже нигде не вызывается сейчас — раньше вешался через @input="inputTitle" на <input> в App.vue
    inputTitle(event) {
      // event.target.value — обычное DOM-свойство, значение поля ввода в момент события
      this.title = event.target.value;
    },

    /*Аналогично inputTitle, но для второго поля*/
    inputBody(event) {
      this.body = event.target.value;
    },
    sayHello() {
      console.log('Привет из sayHello!');
    }
  },
}
</script>

<style>
/* Звёздочка * — универсальный CSS-селектор, применяет правило ко ВСЕМ элементам страницы.
   Это глобальный сброс отступов и box-sizing — стандартная практика в начале проекта */
* {
  box-sizing: border-box; /* ширина/высота элемента считается вместе с padding и border */
  margin: 0;
  padding: 0;
}

.app {
  padding: 50px;
}
</style>