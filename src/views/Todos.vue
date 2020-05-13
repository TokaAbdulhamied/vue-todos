<template>
  <div >
    <TodoList status="active"/>
  </div>
</template>

<script>
// @ is an alias to /src
  import TodoList from "../components/TodoList"
export default {
  name: "Todos",
  components: {
    TodoList
  }
};
</script>
