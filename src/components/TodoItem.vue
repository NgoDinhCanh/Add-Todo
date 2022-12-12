<template>
  <p :class="['todo-item', todoProps.completed ? 'is-completed' : '']">
    <input
      type="checkbox"
      :checked="todoProps.completed"
      @change="markItemComplete"
    />
    {{ todoProps.title }}
    <button class="btn-delete" @click="deleteItem">Delete</button>
  </p>
</template>

<script>
export default {
  name: "TodoItem",
  props: ["todoProps"],
  setup(props, context) {
    const markItemComplete = () => {
      context.emit("item-completed", props.todoProps.id);
    };
    const deleteItem = () => {
      context.emit("item-deleted", props.todoProps.id);
    };
    return {
      markItemComplete,
      deleteItem,
    };
  },
};
</script>

<style>
.btn-delete {
  background: red;
  color: white;
  border: none;
  float: right;
}
.todo-item {
  background: #f4f4f4;
  padding: 10px;
  margin: 0;
  border-bottom: 1px #ccc dotted;
}
.is-completed {
  text-decoration: line-through;
}
</style>
