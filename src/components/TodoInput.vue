<template>
  <div class="input-wrapper">
    <form action="" v-on:submit.prevent="saveNewItem">
      <div class="form-group">
        <label for="todo-input">New TODO item</label>
        <input id="todo-input" type="text" class="form-control" v-model="newTodo" placeholder="start typing a new item..." ref="todoInput" />
        <button class="btn btn-primary">Save</button>
      </div>
    </form>
  </div>
</template>

<script>
// import * as utilities from '../store';

export default {
  name: 'TodoInput',
  props: [''],
  data () {
    return {
      newTodo: ''
    };
  },
  methods: {
    saveNewItem: function (evt) {
      if (this.newTodo !== '') {
        this.$emit('saveTodo', this.newTodo);
        this.newTodo = '';
      }
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.input-wrapper {
  margin-bottom: 2rem;
}
.form-group {
  position: relative;
}
.form-group .btn{
  float: right;
  margin-top: -38px;
}
</style>
