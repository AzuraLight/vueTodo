<template lang="">
<div id="app">
  <TodoHeader></TodoHeader>
  <TodoInput v-on:addTodo="addTodo"></TodoInput>
  <TodoList v-bind:propsdata="todoItems" @removeTodo="removeTodo"></TodoList>
  <TodoFooter v-on:removeAll="clearAll"></TodoFooter>
</div>
</template>
<script>
import TodoHeader from './components/TodoHeader.vue';
import TodoInput from './components/TodoInput.vue';
import TodoList from './components/TodoList.vue';
import TodoFooter from './components/TodoFooter.vue';

export default {
  data() { 
    return {
      todoItems:[]
    }
  },
  created() { 
        if (localStorage.length > 0) { 
            for (let i = 0; i < localStorage.length; i++) { 
                const item = JSON.parse(localStorage.getItem(localStorage.key(i)));
                this.todoItems.push(item);
            }
        }
    },
  methods: {
    addTodo(todoItem) {
      let value = todoItem.text.trim();
      localStorage.setItem(value, JSON.stringify({ text: value }));
      this.todoItems.push({ text: value });
    },
    clearAll() { 
      localStorage.clear();
      this.todoItems = [];
    },
    removeTodo(todoItem, index) { 
      const text = todoItem.text;
      localStorage.removeItem(text);
      this.todoItems.splice(index, 1);
    }   
  },

  components: {
    'TodoHeader': TodoHeader,
    'TodoInput': TodoInput,
    'TodoList': TodoList,
    'TodoFooter': TodoFooter,
  }
}
</script>
<style>
    body {
        text-align: center;
        background-color: #F6F6F8;
    }
    input {
        border-style: groove;
        width: 200px;
    }
    button {
        border-style: groove;
    }
    .shadow {
        box-shadow: 5px 10px 10px rgba(0,0,0,0.03)
    }
</style>