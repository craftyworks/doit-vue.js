<template>
  <div id="app">
    <TodoHeader></TodoHeader>
    <TodoInput v-on:add="addTodo" v-bind:edit-todo-item="selectedItem"></TodoInput>
    <TodoList v-bind:todoItems="todoItems" v-on:remove="removeItem" v-on:edit="editItem"></TodoList>
    <TodoFooter v-on:clear="clearAll"></TodoFooter>
  </div>
</template>

<script>
  import TodoHeader from "./components/TodoHeader";
  import TodoInput from "./components/TodoInput";
  import TodoList from "./components/TodoList";
  import TodoFooter from "./components/TodoFooter";

  export default {
    components: {
      'TodoHeader': TodoHeader,
      'TodoInput': TodoInput,
      'TodoList' : TodoList,
      'TodoFooter': TodoFooter
    },
    data: function () {
      return {
        todoItems: [],
        selectedItem: ''
      }
    },
    methods: {
      removeItem: function (item, index) {
        console.log(item, index)
        this.todoItems.splice(index, 1)
        localStorage.removeItem(item)
      },
      editItem: function(item, index) {
        this.selectedItem = item
      },
      addTodo: function (item) {
        this.todoItems.push(item)
        localStorage.setItem(item, item)
      },
      clearAll: function () {
        this.todoItems.splice(0, this.todoItems.length)
        localStorage.clear()
      }
    },
    created() {
      let length = localStorage.length
      for(let i = 0; i < length; i++) {
        this.todoItems.push(localStorage.key(i))
      }
    }

  }
</script>

<style>
  body {
    text-align: center;
    background-color: #f6f6f8;
  }
  input {
    border-style: groove;
    width: 200px;
  }
  button {
    border-style: groove;
  }
  .shadow {
    box-shadow: 5px 10px 10px rgba(0,0,0,0.03);
  }
</style>
