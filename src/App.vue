<template>
  <div id="app" class="container">
    <TodoInput @saveTodo="addNewTodo"/>
    <TodoList v-bind:todos="filteredTodos" @removeTodo="removeTodo" @changeVisibility="changeVisibility" />
    <!-- <TodoList v-bind:todos="all(todos)" /> -->
    <!-- <ul class="todo-list list-group">
      <li class="todo-list-item list-group-item" v-bind:key="todo.id" v-for="todo in filteredTodos" v-bind:class="{completed: todo.completed}">
        <p class="item">
          {{todo.title}}
        </p>
      </li>
    </ul> -->
    <!-- using filters: -->
    <!-- {{ todos | active }} -->
  </div>
</template>

<script>
// import * as utilities from './store'
import TodoInput from './components/TodoInput.vue';
import TodoList from './components/TodoList.vue';
// import store from './store.js'

var filters = {
  all: function (todos) {
    return todos;
  },
  active: function (todos) {
    console.log(todos, 'todos');
    return todos.filter(function (item) {
      return !item.completed;
    });
  },
  completed: function (todos) {
    return todos.filter(function (item) {
      return item.completed;
    });
  }
};

export default {
  name: 'App',
  components: {
    TodoList,
    TodoInput
  },
  data () {
    return {
      todos: [
        {
          id: 1,
          title: 'Todo one',
          completed: false
        },
        {
          id: 2,
          title: 'Todo two',
          completed: true
        },
        {
          id: 3,
          title: 'Todo three',
          completed: false
        }
      ],
      nextID: 4,
      visibility: 'all'
    };
  },
  computed: {
    pluralise: function (n) {
      return n;
    },
    filteredTodos: function () {
      return filters[this.visibility](this.todos);
    }
  },
  methods: {
    addNewTodo: function (val) {
      console.log(val, 'addNewTodo event data');
      this.todos.push({
        id: this.nextID,
        title: val
      });
      this.nextID++;
    },
    removeTodo: function (id) {
      console.log(id, 'remove id');
      this.todos = this.todos.filter(function (item) {
        return item.id !== id;
      });
    },
    changeVisibility: function (newVal) {
      this.visibility = newVal;
    }
  }
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
