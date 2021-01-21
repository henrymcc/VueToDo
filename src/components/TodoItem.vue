<template>
  <p class="item">
    <input type="checkbox" :id="'todo-item' + todo.id" v-model="todo.completed"/>
    <label :for="'todo-item' + todo.id">{{todo.title}}</label>
    <button v-on:click="deleteTodo" class="btn btn-del">x</button>
  </p>
</template>

<script>
export default {
  name: 'TodoItem',
  props: ['todo'],
  components: {},
  methods: {
    deleteTodo: function (evt) {
      console.log(evt, 'delete todo data');
      this.$emit('removeTodo', this.todo.id);
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
p {
  margin: 0;
  display: flex;
  align-items: center;
}
input[type=checkbox] {
  margin-right: 1rem;
}
label {
  margin: 0;
}
.btn-del {
  margin-left: auto;
}
.completed .btn-del {
  color: #FFF;
}
.completed label{
  text-decoration: line-through;
}
</style>
