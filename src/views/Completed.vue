<template>
  <div class="home">
    <TodoList status="completed"/>
  </div>
</template>

<script>
// @ is an alias to /src
  import TodoList from "../components/TodoList"
export default {
  name: "Completed",
  components: {
    TodoList
  }
};
</script>