<template>
  <div id="todo-list-example">
  <form v-on:submit.prevent="submitAction">
    <div>
    <label>Add a todo</label>
    <input
      v-model="newTodoText"
      id="new-todo"
      placeholder="Ex. Study VueJS"
    >
    <button v-if="!isEditing">Add</button>
    <button v-else>Edit</button>
      <div>
        <span id='validate-field-text' v-if="showValidateTodoText">Todo can't be empty!</span>
      </div>
    </div>
  </form>
  <ul id='align-center'>
    <li
      v-for="(todo, index) in todos"
      v-bind:key="todo.id"
    >{{todo.title}}
      <button v-on:click='editTodo(index, todo.title)'>Edit</button>
      <button v-on:click='removeTodo(index)'>Remove</button>
    </li>
    
  </ul>
</div>
</template>

<script>
export default {
  name: 'TodoList',
  data() {
    return {
    newTodoText: '',
    showValidateTodoText: false,
    isEditing: false,
    editingIndex: null,
    todos: [
      {
        id: 1,
        title: 'Do the dishes',
      },
      {
        id: 2,
        title: 'Take out the trash',
      },
      {
        id: 3,
        title: 'Study more VueJS'
      }
    ],
    nextTodoId: 4
    };
  },
  methods: {
    submitAction: function () {
      if (this.newTodoText.length > 0) {
        if (this.isEditing) {
          this.todos.splice(this.editingIndex, 1, {id: this.nextTodoId++, title:this.newTodoText})
        } else {
          this.todos.push({
            id: this.nextTodoId++,
            title: this.newTodoText
          })
        }
        this.newTodoText = ''
        this.showValidateTodoText = false
        this.isEditing = false
      } else {
        this.showValidateTodoText = true
      }
    },
    removeTodo: function(index) {
      this.todos.splice(index, 1)
    },
    editTodo: function(index, text) {
      this.newTodoText = text
      this.isEditing = true
      this.editingIndex = index
    }
  }
}
</script>

<style>
#align-center {
  width: 20%;
  margin-right: auto;
  margin-left: auto;
}

#validate-field-text {
  color: #D52D2D;
  margin-left: 1%;
  font-weight: bold;
}
</style>