<template>
  <div class="task__list">
    <div class="task__header">
        <h3 class="task__header-title">My Tasks</h3>
        <button 
          class="button--link"
          @click="deleteAllTask">
        Delete All
        </button>
    </div>
    <template v-for="(todo, index) in taskList">
      <TodoItem 
        :todo="todo"
        :index="index" 
        :key="todo.id" 
        @deletedTask="deleteTask($event)"/>
    </template>
    <p class="task__message" v-if="taskList.length === 0">You don't have a task</p>
  </div>
</template>

<script>
import TodoItem from './TodoItem'

export default {
  data () {
    return {
      taskList: this.tasks 
    }
  },
  name: 'TodoList',
  props: {
    tasks: Array,
    deleteTask: Function,
    deleteAllTask: Function
  },
  components: {
    TodoItem
  },
  watch: {
    tasks () {
      this.taskList = this.tasks
    }
  }
}
</script>

<style lang="scss" scoped>
@import '../styles/imports';

.task__list {
  background: #fff;
  padding-bottom: $m-size;
  margin-bottom: $m-size;
  border-radius: 10px;
  padding: $m-size $l-size;
  box-shadow: 0 15px 25px rgba(0,0,0,.2);
}

.task__message {
  color: $off-white;
  text-align: center;
  padding: $m-size;
  font-size: $m-size;
  font-weight: bold;
}

.task__header { 
  color: $blue;
  display: flex;
  justify-content: space-between;
  align-items: center;
  position: relative;
  padding: 20px 0;

  &:after {
    content: '';
    position: absolute;
    bottom: 0;
    left: 0;
    right: 0;
    margin: auto;
    width: 100%;
    height: 1px;
    background: transparentize($off-black, .9);
  }
}

.task__header-title {
  font-size: $m-size;
  margin: 0;
  color: transparentize($off-black, .2);
}

button {
  color: transparentize($off-black, .2);
  background: none;
  padding: 0;
}
</style>
