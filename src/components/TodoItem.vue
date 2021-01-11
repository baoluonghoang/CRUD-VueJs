<template>
    <div class="todo-item" v-bind:class="{'is-completed' : todoItem.completed}">
        <input type="checkbox" v-on:change="markComplete()">
        {{todoItem.title}}
        <button 
            class="del"
            v-on:click="$emit('del-todo', todoItem.id)"
        >
        Delete
        </button>
        <button
            class="edit"
            v-on:click="updateItem"
        >
        Update
        </button>
    </div>
</template>

<script>
export default {
    name: "TodoItem",
    //can't change a prop from inside a component
    props: ["todoItem"],
    data() {
        return {
            item: this.todoItem
        }
    },
    methods: {
        markComplete() {
            this.item.completed = !this.item.completed;
        },
        updateItem() {
            var data = {
                id: this.todoItem.id,
                title: this.todoItem.title,
                completed: this.todoItem.completed
            }

            this.$emit('edit-todo', data);
            return data;
        } 
    }
}
</script>

<style scoped>
    .todo-item {
        padding: 10px 20px;
    }

    .is-completed {
        text-decoration: line-through;
    }

    .edit {
        text-decoration: none;
        background: green;
        color: #ffffff;
        border: none;
        padding: 5px 9px;
        border-radius: 50%;
        cursor: pointer;
        float: right;
    }
    .del {
        text-decoration: none;
        background: #ff0000;
        color: #ffffff;
        border: none;
        padding: 5px 9px;
        border-radius: 50%;
        cursor: pointer;
        float: right;
    }
</style>