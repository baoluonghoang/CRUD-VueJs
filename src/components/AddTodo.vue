<template>
  <form>
    <input
      v-if="checkEdit == 1"
      type="text"
      id="input-add"
      v-model="titleEdit.title"
    />
    <input
      v-else
      type="text"
      id="input-add"
      v-model="title"
      placeholder="Input here..."
    />
    <button
      v-if="checkEdit == -1"
      type="submit"
      id="input-submit"
      v-on:click.prevent="onAdd"
    >
      Add
    </button>
    <button
      v-else
      type="submit"
      id="input-submit"
      v-on:click="onSave"
      :disabled="titleEdit.title != '' ? disabled : ''"
    >
      Save
    </button>
    <div v-if="titleEdit.title == ''">Bạn không được để trống!</div>
  </form>
</template>

<script>
import { v4 as uuidv4 } from "uuid";

export default {
  name: "AddTodo",
  data() {
    return {
      title: "",
      titleEdit: "",
      isWarning: true
    };
  },
  props: ["checkEdit", "itemTitle"],
  watch: {
    //watch props in Vue3
    itemTitle: function(newVal) {
      // watch it
      this.titleEdit = newVal;
    },
  },
  methods: {
    onAdd() {
      const newTodo = {
        id: uuidv4(),
        title: this.title,
        completed: false,
      };

      if (this.title === "") {
        alert("Bạn chưa nhập todo!!!");
        return;
      }

      //send up event to parent TodoList
      this.$emit("add-todo", newTodo);
      this.title = "";
    },
    onSave() {
      //send up event to parent TodoList
      this.$emit("submit", this.titleEdit);
    }
  }
};
</script>

<style scoped>
form {
  text-align: center;
  max-width: 50%;
  margin: 0 auto;
}

#input-add {
  padding: 10px 25px 10px 20px;
  outline: none;
  border: 1px solid #dddddd;
}

#input-submit {
  background-color: green;
  color: #ffffff;
  padding: 10px;
  border: none;
  outline: none;
  cursor: pointer;
}

#input-submit:hover {
  background-color: rgb(4, 115, 167);
}
</style>
