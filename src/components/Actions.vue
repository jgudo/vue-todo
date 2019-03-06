<template>
  <div class="add-task">
    <transition name="fade" v-on:after-leave="afterLeave">
      <div class="error__message" ref="error" v-if="errorMessage">
        <p>{{ errorMessage }}</p>
      </div>
    </transition>
    <input 
      @input="onChange" 
      @keyup.enter="addTask" 
      type="text"
      :value="inputValue"
      placeholder="Enter task here" >
    <button @click="onAddTask">+</button>
  </div>
</template>

<script>
export default {
  name: 'Actions',
  data () {
    return {
      errorMessage: undefined,
      errorVisible: false,
      inputValue: this.input
    }
  },
  props: {
    addTask: Function,
    input: String
  },
  methods: {
    onChange (e) {
      this.$emit('inputHasChanged', e.target.value)
    },
    onAddTask () {
      if (this.inputValue === '') {
        this.errorVisible = true
        this.errorMessage = 'Please add something on the text field'
      } else {
        this.errorMessage = undefined
        this.addTask()
      }
    },
    afterLeave: function (el) {
      console.log('beforeleave')
      this.errorMessage = undefined
    }
  },
  watch: {
    input () {
      this.inputValue = this.input
    },
    error () {
      this.errorMessage = this.error
    }
  }
}
</script>

<style lang="scss" scoped>
@import '../styles/imports';

button {
  width: 60px;
  height: 60px;
  background: $yellow;
  color: $off-black;
  border-radius: 50%;
  position: absolute;
  left:0;
  right:0; 
  margin: auto;
  z-index: 1;
  bottom: -80px;
  padding: 0;
  font-size: $l-size;
  border-bottom: none;
  box-shadow: 0 10px 20px rgba(0,0,0,.2);

  &:hover {
      background: darken($yellow, 10%);
  }
}

input {
  flex-grow: 1;
  //background: $dark-blue;
  background: transparent;
  border: none;
  border-bottom: .1rem solid rgba(255,255,255,.3);
  padding: $m-size;
  color: #fff;
  margin-right: $m-size;
  font-size: $l-size;
  
  &:focus {
      outline: none;
  }

  &::placeholder {
      font-size: $l-size;
      color: #fff;
  }
  &::-webkit-input-placeholder {
      font-size: $l-size;
      color: #fff;
  }
}

.add-task {
  display: flex;
  //padding: $l-size $m-size 0;
  margin-bottom: $xl-size;
  flex-direction: column;
  position: relative;
}

.error__message {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  width: 35rem;
  padding: $s-size $m-size;
  text-align: center;
  border-radius: 0 0 20px 20px;
  margin: auto;
  opacity: 0;
  transition: all .5s ease;
  transform: translateY(-100%);
  background: #fff;
}

.fade-enter-active {
  animation: show 3s ease;
}

.fade-leave-active {
  animation: none;
}

.fade-enter, .fade-leave-to /* .fade-leave-active below version 2.1.8 */ {
  animation: none
}

@keyframes show {
  0% {
    transform: translateY(-100%);
    opacity: 0;
  }
  10% {
    opacity: 1;
    transform: translateY(0);
  }
  80% {
    opacity: 1;
    transform: translateY(0);
  }
  100% {
    opacity: 0;
    transform: translateY(-100%);
  }
}
</style>
