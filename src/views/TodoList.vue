<template>
  <div class="container">
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
            v-for="(todo, index) in todos"
            :key="index"
            :todo="todo"
            @toggle="toggleTodo(todo)"
            @on-delete="deleteTodo(todo)"
            @on-edit="editTodo(todo, $event)"
            @on-change="saveTodo()"
          />
        </ul>
        <div>
          <button :class="{ active: filter == 'all' }" @click="filter = 'all'">All</button>
          <button :class="{ active: filter == 'active' }" @click="filter = 'active'">Active</button>
          <button :class="{ active: filter == 'completed' }" @click="filter = 'completed'">Completed</button>
      </div>
      </div>
    </div>
  </div>
</template>

<script>
import Todo from "../components/Todo";

export default {
  props: {
    listName: String
  },
  data() {
    return {
      newTodo: "",
      filter :'all',
      todos: [
                {  description: "Do the dishes", completed: false },
        {  description: "Take out the trash", completed: true },
        {  description: "Finish doing laundry", completed: false }
      ]
    };
  },
  mounted() {
    if (localStorage.getItem('todos')) {
      try {
        this.todos = JSON.parse(localStorage.getItem('todos'));
      } catch(e) {
        localStorage.removeItem('todos');
      }
    }
  },
  computed:{
        todosFiltered () {
      if (this.filter == 'all') {
        return this.todos
      } else if (this.filter == 'active') {
        return this.todos.filter(todo => !todo.completed)
      } else if (this.filter == 'completed') {
        return this.todos.filter(todo => todo.completed)
      }
      return this.todos
    }
  },
  methods: {
    addTodo() {
      if (this.newTodo.length > 0) {
        this.todos.push({
          description: this.newTodo,
          completed: false,
        });
        this.saveTodo()
      }
      this.newTodo = "";
    },
    deleteTodo(deletedTodo) {
      this.todos = this.todos.filter(todo => todo !== deletedTodo);
      this.saveTodo()
    },
    editTodo(todo, newTodoDescription) {
      todo.description = newTodoDescription;
      this.saveTodo()
    },
    saveTodo() {
      const parsed = JSON.stringify(this.todos);
      localStorage.setItem('todos', parsed);
    }

 


 
  },
  components: { Todo }
};
</script>

<style scoped lang="scss"></style>
