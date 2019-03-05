<template>
  <div class="todo">
    <input @change="onInputChange" type="text" v-model="inputValue">
    <button @click="addTask">Add Task</button>
    <template v-for="todo in tasks">
      <TodoItem :todo="todo" :key="todo.id" />
    </template>
  </div>
</template>

<script>
import moment from 'moment'
import uuid from 'uuid'

import TodoItem from './components/TodoItem'

export default {
  name: 'App',
  data: function () {
    return {
      inputValue: '',
      tasks: []
    }
  },
  methods: {
    onInputChange (e) {
      const val = e.target.value
      this.inputValue = val
    },
    addTask () {
      this.tasks = [
        ...this.tasks,
        {
          id: uuid(),
          createdAt: moment().valueOf(),
          task: this.inputValue,
          status: 'unfinished' 
        }
      ]
    }
  },
  components: {
    TodoItem
  }
}
</script>

<style scoped>
div {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}

.todo {
  padding: 4rem 2rem;
}

</style>
