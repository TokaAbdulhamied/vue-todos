<template>
  <div class="container">
    <div class="row">
      <div class="col-12 py-5">
        <h1>{{ listName }}</h1>
      </div>
    </div>
    <div class="row mb-3 ">
      <form
        class="col-12 col-sm-10 col-md-8 cl-lg-6"
        @submit.prevent="addTodo()"
      >
        <input
          v-model="newTodo"
          type="text"
          class="form-control"
          placeholder="Create a new to-do..."
        />
      </form>
    </div>
    <div class="row">
      <div class="col-12 col-sm-10 col-lg-6  ">
        <ul class="list-group">
          <todo
            v-for="todo in todos"
            :key="todo.id"
            :todo="todo"
            @toggle="toggleTodo(todo)"
            @on-delete="deleteTodo(todo.id)"
            @on-edit="editTodo(todo, $event)"
          />
        </ul>
      </div>
    </div>
  </div>
</template>

<script>
import Todo from "./Todo.vue";

export default {
  props: {
    listName: String
  },
  data() {
    return {
      newTodo: "",
      nextTodo: 4,
      todos: [
        { id: 1, description: "Do the dishes", completed: false },
        { id: 2, description: "Take out the trash", completed: true },
        { id: 3, description: "Finish doing laundry", completed: false }
      ]
    };
  },
  methods: {
    addTodo() {
      if (this.newTodo.length > 0) {
        this.todos.push({
          id: this.nextTodo,
          description: this.newTodo,
          completed: false
        });
        this.newTodo++;
      }
      this.newTodo = "";
    },
    toggleTodo(todo) {
      todo.completed = !todo.completed;
    },
    deleteTodo(id) {
      this.todos = this.todos.filter(todo => todo.id !== id);
    },
    editTodo(todo, newTodoDescription) {
      todo.description = newTodoDescription;
    }
  },
  components: { Todo }
};
</script>

<style scoped lang="scss"></style>
