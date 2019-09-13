<template>
  <div>
    <p class="tasks">完了タスク: {{  this.todos.filter(todo => todo.done === true).length }}</p>
    <p class="tasks">保留中タスク: {{ this.todos.filter(todo => todo.done === false).length }}</p>
    <todo v-on:complte-todo="completeTodo" v-on:delete-todo="deleteTodo" v-for="(todo, index) in todos" :key="index" :todo="todo"></todo>
  </div>
</template>

<script type = "text/javascript" >
import Todo from './Todo'
import sweetalert from 'sweetalert'

export default {
  props: ['todos'],
  components: {
    Todo
  },
  methods: {
    async deleteTodo (todo) {
      const willDelete = await sweetalert({
        title: 'Are you sure?',
        text: 'If you delete this post all associated comments also deleted permanently.',
        type: 'warning',
        showCancelButton: true,
        closeOnConfirm: false,
        showLoaderOnConfirm: true,
        confirmButtonClass: 'btn-danger',
        confirmButtonText: 'Yes, delete it!'
      })
      if (willDelete) {
        const todoIndex = this.todos.indexOf(todo)
        this.todos.splice(todoIndex, 1)
        sweetalert('Deleted!', 'Your To-Do has been deleted.', 'success')
      }
    },
    completeTodo (todo) {
      const todoIndex = this.todos.indexOf(todo)
      this.todos[todoIndex].done = true
      sweetalert('Success!', 'To-Do completed!', 'success')
    }
  }
}
</script>
<style scoped>
p.tasks {
  text-align: center
}
</style>
