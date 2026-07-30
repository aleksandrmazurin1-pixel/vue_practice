<template>
  <div>
    <div>
      <!-- v-for="post in posts" — аналог обычного цикла for...of в JS:
           for (const post of posts) { ... }
           "posts" (множественное число) — проп, пришедший снаружи (из App.vue).
           "post" (единственное число) — имя, которое мы сами придумали для каждого элемента цикла. -->

      <!-- ⚠️ Здесь не хватает :key="post.id" — уникального идентификатора для Vue,
           чтобы он понимал, какой DOM-элемент к какому объекту массива относится
           при добавлении/удалении элементов. Без него Vue выдаст предупреждение в консоли. -->
      <div class="post" v-for="post in posts" :key="post.id">
        <!-- {{ post.title }} — интерполяция: подставляет значение поля title
             текущего поста прямо в текст. Реактивна: если posts изменится, текст обновится сам -->
        <div><strong>Header: </strong>{{ post.title }}</div>
        <div><strong>Description: </strong>{{ post.body }}</div>
        <button class="btn" @click="$emit('delete-post', post.id)">Удалить Задачу</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  // props — объявление "входных параметров" компонента, аналог аргументов функции.
  // Это позволяет Vue проверять тип данных и предупреждать в консоли, если передали не то.
  props: {
    posts: {
      type: Array,     // ожидаем именно массив
      required: true   // проп обязателен — без него Vue выдаст предупреждение
    }
  }
}
</script>

<style scoped>
/* "scoped" в теге <style> означает, что эти стили применяются ТОЛЬКО
   к элементам этого конкретного компонента (Vue добавляет уникальный
   data-атрибут ко всем элементам шаблона и селекторам здесь).
   Стили не "утекают" на другие компоненты и не конфликтуют с ними. */
.post {
  padding: 15px;
  border: 2px solid #439019;
  margin-top: 10px;
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
</style>