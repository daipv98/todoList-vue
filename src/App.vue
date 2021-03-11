<template>
    <div id="app">
      <component-todoList></component-todoList>
      
    </div>
</template>

<script>
import ComponentTodoList from './components/TodoList'
export default {
  name: 'App',
  data() {
    return {
      msg: 'hello VueJS'
    }
  },
  components: {
    ComponentTodoList
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>