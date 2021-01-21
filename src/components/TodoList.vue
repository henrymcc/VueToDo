<template>
  <div class="item-wrapper">
    <div class="todo-counter">
      <span>{{remainderCount}}</span> items left
    </div>
    <div class="filters">
      <button class="btn btn-filter btn-outline-secondary" v-on:click="changeVisibility('all')">All</button>
      <button class="btn btn-active btn-outline-secondary" v-on:click="changeVisibility('active')">Active</button>
      <button class="btn btn-completed btn-outline-secondary" v-on:click="changeVisibility('completed')">Completed</button>
    </div>
    <div class="mark-completed form-group">
      <input id="mark-complete" type="checkbox" class="" v-model="toggleComplete" />
      <label for="mark-complete">Toggle Completed</label>
    </div>
    <ul class="todo-list list-group">
      <li class="todo-list-item list-group-item" v-bind:key="todo.id" v-for="todo in todos" v-bind:class="{completed: todo.completed}">
        <TodoItem v-bind:todo="todo" @removeTodo="removeTodo"/>
      </li>
    </ul>
  </div>
</template>

<script>
import TodoItem from './TodoItem.vue';

export default {
  name: 'TodoList',
  props: ['todos'],
  data () {
    return {};
  },
  components: {
    TodoItem
  },
  computed: {
    remainderCount: function () {
      return this.todos.filter(function (item) {
        return !item.completed;
      }).length;
    },
    toggleComplete: {
      get: function () {
        return this.remainderCount === 0;
      },
      set: function (val) {
        this.todos.forEach(element => {
          element.completed = val;
        });
      }
    }
  },
  methods: {
    removeTodo: function (id) {
      this.$emit('removeTodo', id);
    },
    changeVisibility: function (newVal) {
      console.log(newVal, 'newVal');
      this.$emit('changeVisibility', newVal);
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.todo-counter {
  margin-bottom: 1rem;
}
.filters {
  display: flex;
  margin-bottom: 1rem;
}
.filters .btn {
  margin: 0 1rem;
}
.filters .btn:first-of-type {
  margin: 0 1rem 0 0;
}
</style>
