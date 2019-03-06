<template>
  <div class="container">
    <Actions 
      @inputHasChanged="onInputChange($event)" 
      :addTask="addTask" 
      :input="inputValue"/>
    <TodoList 
      :deleteTask="deleteTask" 
      :tasks="tasks"
      :deleteAllTask="deleteAllTask"/>
  </div>
</template>

<script>
import moment from 'moment'
import uuid from 'uuid'

import Actions from './components/Actions'
import TodoList from './components/TodoList'

export default {
  name: 'App',
  data () {
    return {
      inputValue: '',
      tasks: []
    }
  },
  created () {
    if ('localStorage' in window && localStorage.tasks) {
      this.tasks = JSON.parse(localStorage.getItem('tasks'))
    }
  },
  methods: {
    onInputChange (e) {
      this.inputValue = e
    },
    addTask () {
      if (this.inputValue !== '') {
        this.tasks = [
          {
            id: uuid(),
            createdAt: moment().valueOf(),
            task: this.inputValue
          },
          ...this.tasks
        ]
      } 
      this.inputValue = ''
    },
    deleteTask (id) {
      this.tasks = this.tasks.filter((task) => {
        return task.id !== id
      })
    },
    deleteAllTask () {
      this.tasks = []
    }
  },
  components: {
    Actions,
    TodoList
  },
  watch: {
    tasks () {
      if ('localStorage' in window) {
        localStorage.setItem('tasks', JSON.stringify(this.tasks))
      }
    }
  }
}
</script>

<style lang="scss">
@import './styles/imports';

.container {
  max-width: 60rem;
  margin: 0 auto;
  padding: $xl-size $m-size $xl-size $m-size;
}

</style>
