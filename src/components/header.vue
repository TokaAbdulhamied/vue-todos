<template>
  <header>
      <div class=" header">
        <h3>To Do List</h3>
        <div id="nav">
        <router-link to="/">All</router-link> |
        <router-link to="/todos">Todos</router-link> |
        <router-link to="/completed">Done Todos</router-link>
        </div>
      </div>
  </header>
</template>

<script>
export default {
    name:"Header"
};
</script>

<style lang="scss">
  .header {
    margin-bottom: 20px;
    background: #333;
    color: #fff;
    display: flex;
    justify-content: space-evenly;
    padding: 10px;
   
  }

#nav {
  padding: 5px;

  a {
    color:lightgoldenrodyellow;
    text-decoration: none;
    font-size: 1.3em;
    margin-right: 10px;

    &.router-link-exact-active {
      color: #42b985;
    }
  }
}
</style>