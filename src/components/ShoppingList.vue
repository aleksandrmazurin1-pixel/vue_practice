<template>
  <div class="inner-mars">
    <b>У тебя {{ shoppingList.length }} постов</b>
  </div>

  <form @submit.prevent>
    <div>

      <input type="text" v-model="newItemName">
      <button @click="addToShoppingList">Добавить задачу</button>

    </div>
  </form>

  <card v-for="list in shoppingList" :key="list.id">
    {{ list.name }}
    <button @click="deleteList(list.id)">DELETE</button>
  </card>

</template>

<script>
import Card from "@/components/Card.vue";

export default {
  components: {
    Card,
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
    }
  },
  methods: {
    addToShoppingList() {
      if (this.newItemName !== '') {
        const newItem = {
          id: crypto.randomUUID(),
          name: this.newItemName,
        }
        this.shoppingList.push(newItem);
        this.newItemName = '';
      }
    },

    deleteList(listId) {
      this.shoppingList = this.shoppingList.filter(list => list.id !== listId);
    },
  }
}
</script>

<style>

.inner-mars {
  margin-top: 20px;
  background-color: #d3d3d3;
}
</style>
