<template>
  <div class='ui centered card'>
    <div class="content" v-show="!isEditing">
      <div class='header'>
           {{ todo.title }}
      </div>
      <div class='meta'>
          {{ todo.project }}
      </div>
      <div class='extra content'>
          <span class='right floated edit icon' @click="showForm">
          <i class='edit icon'></i>
        </span>
        <span class='right floated trash icon' @click="deleteTodo(todo)">
          <i class='trash icon'></i>
        </span>
      </div>
    </div>
    <div class="content" v-show="isEditing">
      <div class='ui form'>
        <div class='field'>
          <label>タイトル</label>
          <input type='text' v-model="todo.title">
        </div>
        <div class='field'>
          <label>プロジェクト</label>
          <input type='text' v-model="todo.project">
        </div>
        <div class='ui two button attached buttons'>
          <button class='ui basic blue button' @click="hidenForm">
            追加
          </button>
        </div>
      </div>
    </div>
    <div class='ui bottom attached green basic button' v-show="!isEditing && todo.done">
        完了
    </div>
    <div class='ui bottom attached red basic button' v-show="!isEditing && !todo.done" @click="completeTodo(todo)">
        保留中
    </div>
  </div>
</template>

<script type="text/javascript">
export default {
  props: ['todo'],
  data () {
    return {
      isEditing: false
    }
  },
  methods: {
    hidenForm () {
      this.isEditing = false
    },
    showForm () {
      this.isEditing = true
    },
    deleteTodo (todo) {
      this.$emit('delete-todo', todo)
    },
    completeTodo (todo) {
      this.$emit('complte-todo', todo)
    }
  }
}
</script>
