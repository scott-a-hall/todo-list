<template>
  <div>
    <md-card-header>
      <div class="title">ToDo List</div>
    </md-card-header>
    <md-card>
      <md-field>
        <md-input v-model="currentTodo" @keydown.enter="addTodo()" placeholder=" Add a todo" />
      </md-field>
      <ul class="todos">
        <li v-for="todo in todos" :key="todo.id">
          <md-input type="text" v-model="todo.label" placeholder="update todo">
            <span
              v-if="todo.editing === false"
              class="editing"
              :class="{editing: todo == editedTodo}"
              @dblclick="editTodo(todo)"
            >{{ todo.label }}</span>
          </md-input>
          <input type="checkbox" @change="completeTodo(todo)" :checked="todo.isComplete" />
          <md-button class="md-raised" @click="removeTodo(todo)">Delete</md-button>
        </li>
      </ul>
    </md-card>
  </div>
</template>

<script>
export default {
  data() {
    return {
      todos: [],
      currentTodo: "",
      completed: "",
      editedTodo: "",
    };
  },
  methods: {
    addTodo() {
      this.todos.push({
        id: this.todos.length,
        label: this.currentTodo,
        completed: false,
        editing: false,
      });
      this.currentTodo = "";
    },
    completeTodo(todo) {
      todo.isComplete = !todo.isComplete;
    },
    editTodo(todo) {
      const index = this.todos.indexOf(todo);
      this.todos[index].editing = !this.todos[index].editing;
    },
    removeTodo(todo) {
      var index = this.todos.indexOf(todo);
      this.todos.splice(index, 1);
    },
  },
};
</script>

<style>
.title {
  font-size: 48px;
  text-align: center;
  margin-top: 20px;
  margin-bottom: 10px;
  color: #006a6a;
}
.md-card {
  width: 50%;
  margin-left: auto;
  margin-right: auto;
}
ul {
  list-style: none;
}
.md-button {
  color: red;
}
li {
  display: flex;
  padding-top: 5px;
  padding-bottom: 5px;
}
</style>
