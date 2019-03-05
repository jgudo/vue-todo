<template>
  <div class="todo__item"> 
    <h1>{{ todo.task }}</h1>
    <span>Created at: {{ createdAt(todo.createdAt) }}</span>
    <span>Status: {{ todo.status }}</span>
  </div>
</template>

<script>
import moment from 'moment'

export default {
  name: 'TodoItem',
  methods: {
    createdAt (date) {
      return moment(date).format('LL')
    }
  },
  props: {
    todo: {
      task: String,
      createdAt: Number,
      id: String,
      status: String
    }
  }
}
</script>
