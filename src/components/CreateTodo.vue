<template>
  <div class='ui basic content center aligned segment'>
    <button class='ui basic button icon' v-on:click="openForm" v-show="!isCreating">
      <i class='plus icon'></i>
    </button>
    <div class='ui centered card' v-show="isCreating">
      <div class='content'>
        <div class='ui form'>
          <div class='field'>
            <label>タイトル</label>
            <input v-model="titleText" type='text'>
          </div>
          <div class='field'>
            <label>プロジェクト</label>
            <input v-model="projectText" type='text'>
          </div>
          <div class='ui two button attached buttons'>
            <button class='ui basic blue button' @click="createForm">
              追加
            </button>
            <button class='ui basic red button' @click="closeForm">
              キャンセル
            </button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data () {
    return {
      titleText: '',
      projectText: '',
      isCreating: false
    }
  },
  methods: {
    openForm () {
      this.isCreating = true
    },
    closeForm () {
      this.isCreating = false
    },
    createForm () {
      if (this.titleText.length > 0 && this.projectText.length > 0) {
        const title = this.titleText
        const project = this.projectText
        this.$emit('create-todo', {
          title,
          project,
          isCreating: false,
          done: false
        })
        this.titleText = ''
        this.projectText = ''
        this.isCreating = false
      }
    }
  }
}
</script>
