<template>
  <div id="app">
    <h1 class="ui dividing centered header">Vue.js Todoアプリ</h1>
    <div class='ui three column centered grid'>
      <div class='column'>
        <todo-list :todos="todos"></todo-list>
        <create-todo v-on:create-todo="createTodo"></create-todo>
      </div>
    </div>
  </div>
</template>

<script>
import sweetalert from 'sweetalert'
import TodoList from './components/TodoList'
import CreateTodo from './components/CreateTodo'

export default {
  name: 'app',
  components: {
    TodoList,
    CreateTodo
  },
  data () {
    return {
      todos: [{
        title: 'タイトル A',
        project: 'プロジェクト A',
        done: false
      }, {
        title: 'タイトル B',
        project: 'プロジェクト B',
        done: true
      }, {
        title: 'タイトル C',
        project: 'プロジェクト C',
        done: false
      }, {
        title: 'タイトル D',
        project: 'プロジェクト D',
        done: false
      }]
    }
  },
  methods: {
    createTodo (newTodo) {
      this.todos.push(newTodo)
      sweetalert('Success!', 'To-Do created!', 'success')
    }
  }
}
</script>
