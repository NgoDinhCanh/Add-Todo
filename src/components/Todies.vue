<template>
  <AddTodo @add-todo="addTodo" />
  <TodoItem
    v-for="todo in todies"
    :key="todo.id"
    :todoProps="todo"
    @item-completed="markComplete"
    @item-deleted="deleteTodo"
  />
</template>

<script>
import { ref } from "vue";
import TodoItem from "./TodoItem.vue";
import AddTodo from "./AddTodo.vue";
import axios from "axios";
export default {
  name: "Todies",
  components: { TodoItem, AddTodo },
  setup() {
    const todies = ref([]);

    const getAllTodies = async () => {
      try {
        const res = await axios.get(
          "https://jsonplaceholder.typicode.com/todos?_limit=5"
        );
        todies.value = res.data;
      } catch (error) {
        console.log(error);
      }
    };
    getAllTodies();
    const markComplete = (id) => {
      todies.value = todies.value.map((todo) => {
        if (todo.id === id) todo.completed = !todo.completed;
        return todo;
      });
    };
    const deleteTodo = async (id) => {
      try {
        await axios.delete(`https://jsonplaceholder.typicode.com/todos/${id}`);
        todies.value = todies.value.filter((todo) => todo.id !== id);
      } catch (error) {
        console.log(error);
      }
    };
    const addTodo = async (newTodo) => {
      try {
        const res = await axios.post(
          "https://jsonplaceholder.typicode.com/todos",
          newTodo
        );
        todies.value.push(res.data);
      } catch (error) {
        console.log(error);
      }
    };
    return {
      todies,
      markComplete,
      deleteTodo,
      addTodo,
    };
  },
};
</script>

<style></style>
