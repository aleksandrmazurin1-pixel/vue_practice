<template>
  <div>
    <!-- @submit.prevent — сокращение для @submit="event => event.preventDefault()".
         .prevent — модификатор события, автоматически вызывает preventDefault(),
         чтобы страница не перезагружалась при отправке формы (стандартное поведение <form> в HTML) -->
    <form @submit.prevent>
      <h4> Создание поста</h4>

      <!-- v-model="post.title" — двусторонняя привязка (сахар сразу для двух вещей):
           1) :value="post.title"                          — вывести текущее значение в поле
           2) @input="post.title = $event.target.value"    — при вводе записать новое значение обратно
           Это как раз то, что вручную было реализовано в App.vue через inputTitle(event) -->

      <!-- ✅ ИСПРАВЛЕНО: раньше data() ниже возвращала плоские title/body без объекта post,
           а здесь использовалось v-model="post.title" — то есть Vue пытался обратиться
           к несуществующему post.title (post был undefined), и это ломало компонент.
           Теперь data() возвращает { post: { title, body } } — структура совпадает
           с тем, что ожидает шаблон, ошибка "Cannot read properties of undefined" уйдёт. -->
      <input
          v-model="post.title"
          class="inp"
          type="text"
          placeholder="Введите название"
      >
      <input
          v-model="post.body"
          class="inp"
          type="text"
          placeholder="Введите oписание"
      >

      <!-- Обычная кнопка. Внутри <form> кнопка без type="button" по умолчанию
           имеет type="submit" — именно поэтому клик по ней триггерит @submit.prevent выше -->
      <button
          class="btn">
        Добавить
      </button>
    </form>
  </div>
</template>

<script>
export default {
  data() {
    return {
      // ✅ ИСПРАВЛЕНО: title и body теперь вложены в объект post,
      // чтобы совпадать с post.title / post.body, которые используются
      // в v-model выше. Раньше это были два отдельных плоских поля (title, body)
      // без общей обёртки — из-за чего "post" в шаблоне ссылался в никуда.
      post: {
        title: "",
        body: "",
      }
    }
  }

  // ⚠️ Момент, который всё ещё не решён (это отдельная задача, не текущий баг):
  // даже сейчас кнопка "Добавить" ничего не отправляет обратно в App.vue —
  // данные из этого компонента никак не попадают в posts. Для этого понадобится
  // $emit (кастомные события) — разберём это отдельно, когда дойдёт очередь.
}
</script>

<style scoped>
.inp {
  margin-top: 10px;
  width: 100%;
  border: 2px solid #285a0d;
  padding: 10px 10px;
}

.btn {
  background-color: #439019;
  color: #fff;
  font-weight: bold;
  border-radius: 30px;
  padding: 8px 15px;
  border: none;
  margin-top: 10px;
  margin-bottom: 20px;
}
</style>