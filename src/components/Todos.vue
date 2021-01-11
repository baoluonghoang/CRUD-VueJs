<template>
  <div class="border-todo">
    <div v-if="todos == ''" class="danger">
        Bạn chưa nhập todo nào
    </div>
    <div class="v-else">
        <div v-bind:key="todo.id" v-for="todo in todos" >
      <TodoItem
        v-bind:todoItem="todo"
        v-on:del-todo="$emit('del-todo', todo.id)"
        v-on:edit-todo="updateList"
      />
    </div>
    </div>
  </div>
</template>

<script>
import TodoItem from "./TodoItem";
export default {
  name: "Todos",
  props: ["todos"],
  components: {
    TodoItem,
  },
  methods: {
    updateList(data) {
      
      this.$emit("edit-todo-list", data);
      return;
    },
  },
};
</script>

<style scoped>
.border-todo {
  border: 2px solid #000000;
  max-width: 100%;
  margin: 0 auto;
  margin-top: 10px;
}

.danger {
  color: red;
  text-align: center;
}
</style>