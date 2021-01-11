<template>
  <div class="todoList">
    <AddTodo
      v-on:add-todo="onAddTodo"
      v-bind:checkEdit="checkEdit"
      v-bind:itemTitle="itemEdit"
      v-on:submit="onSaveTodo"
    />
    <Todos
      v-bind:todos="todos"
      v-on:del-todo="onDelete"
      v-on:edit-todo-list="onUpdate"
    />
  </div>
</template>

<script>
import Todos from "../components/Todos";
import AddTodo from "../components/AddTodo";
import axios from "axios";

export default {
  name: "TodoList",
  components: {
    Todos,
    AddTodo,
  },
  data() {
    return {
      url: "https://jsonplaceholder.typicode.com/posts",
      todos: [],
      checkEdit: -1,
      itemEdit: "",
    };
  },
  //get data from json API
  created() {
    axios
      .get(`${this.url}?_limit=5`)
      .then((res) => (this.todos = res.data))
      .catch((err) => console.log(err));
  },
  methods: {
    onDelete(id) {
      // this.todos = this.todos.filter(todo => todo.id !== id);
      axios
        .delete(`${this.url}/${id}`)
        .then((res) => {
          this.todos = this.todos.filter((todo) => todo.id != id);
          return res;
        })
        .catch((err) => console.log(err));
    },

    onAddTodo(newTodos) {
      //not axios API
      // this.todos = [...this.todos, newTodos];
      // console.log(newTodos);
      //destructuring
      const { id, title, completed } = newTodos;

      axios
        .post(`${this.url}`, {
          id: id,
          title: title,
          completed: completed,
        })
        .then((res) => {
          this.todos = [...this.todos, newTodos];
          console.log("lon", newTodos);
          return res;
        })
        .catch((err) => console.log(err));
    },

    onUpdate(data) {
      // this.checkEdit = 1;
      // this.itemEdit = data;
      axios.post(`${this.url}`, data).then((res) => {
        this.checkEdit = 1;
        this.itemEdit = data;
        return res;
      });
    },

    onSaveTodo(data) {
      // let index = this.todos.findIndex((x) => x.id == data.id);
      // this.todos[index].title = data.title;
      // this.checkEdit = -1;
      // this.itemEdit = "";
      axios.post(`${this.url}`, data).then((res) => {
        let index = this.todos.findIndex((x) => x.id == data.id);
        this.todos[index].title = data.title;
        this.checkEdit = -1;
        this.itemEdit = "";
        return res;
      });
    },
  },
};
</script>

<style scoped>
.todoList {
  width: 100%;
  padding: 30px;
  margin: 0 auto;
}
.todoList p {
  text-align: center;
}
</style>
