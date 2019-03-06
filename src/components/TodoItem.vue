<template>
  <div class="task__item"> 
    <div class="task__title">
      <h1>{{ todo.task }}</h1>
      <span>Created at: {{ createdAt(todo.createdAt) }}</span>
    </div>
    <button @click="deleteTask">x</button>
  </div>
</template>

<script>
import moment from 'moment'

export default {
  name: 'TodoItem',
  methods: {
    createdAt (date) {
      return moment(date).format('LL')
    },
    deleteTask () {
      this.$emit('deletedTask', this.todo.id)
    }
  },
  props: {
    todo: {
      task: String,
      createdAt: Number,
      id: String
    },
    index: Number
  }
}
</script>

<style lang="scss" scoped>
@import '../styles/imports';

button {
  background: transparentize($off-black, .5);
  border-bottom: none;
  min-width: 30px;
  min-height: 30px;
  padding: 0;
  color: #fff;
  border-radius: 50%;
  margin-left: $l-size;
  position: relative;
  &:hover {
      background: $off-black;
  }

  div{
      width: 15px;
      height: 1px;
      background: #fff;
      position: absolute;
      top: 0;
      left: 0;
      right: 0;
      bottom: 0;
      margin: auto;
  }
  div:first-child {
      transform: rotate(45deg);
  }
  div:last-child {
      transform: rotate(-45deg);
  }
}

.task__item {
  display: flex;
  justify-content: space-between;
  padding: $l-size 0;
  align-items: center;
  position: relative;

  &:after {
      content: '';
      position: absolute;
      left: 0;
      right: 0;
      bottom: 0; 
      margin: auto;
      width: 85%;
      height: 1px;
      background: transparentize($off-black, .9);

  }

  &:last-child:after{
      background: transparent;
  }
}

.task__title h1 {
  margin-bottom: $s-size;
}

.task__title > span {
  font-size: $s-size;
}
</style>
