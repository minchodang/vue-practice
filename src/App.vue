<template>
  <div id="App">
    <div class="container">
      <div class="col-md-6 offset-md-3">
        <h1 class="text-center mb-4">Todo 어플리케이션</h1>
        <input
          type="text"
          class="form-control"
          v-model="userInput"
          @keyup.enter="addNewTodo"
        />
        <div class="list-group mb-4">
          <template v-for="todo in activeTodoList" :key="todo">
            <Todo :label="todo.label" @componentClick="toggleTodoState(todo)" />
          </template>
        </div>
        <div class="test-right">
          <button
            type="button"
            class="btn btn-sm"
            @click="changeCurrentState('active')"
          >
            할 일
          </button>
          <button
            type="button"
            class="btn btn-sm"
            @click="changeCurrentState('done')"
          >
            완료
          </button>
          <button
            type="button"
            class="btn btn-sm"
            @click="changeCurrentState('all')"
          >
            전체
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Todo from './components/Todo.vue';
export default {
  name: 'App',
  data() {
    return {
      userInput: '',
      todoList: [],
      currentState: 'active',
    };
  },
  computed: {
    activeTodoList() {
      return this.todoList.filter(
        (todo) =>
          this.currentState === 'all' || todo.state === this.currentState
      );
    },
  },
  methods: {
    changeCurrentState(state) {
      this.currentState = state;
    },
    addNewTodo() {
      this.todoList.push({
        label: this.userInput,
        state: 'active',
      });
      this.userInput = '';
    },
    toggleTodoState(todo) {
      todo.state = todo.state === 'active' ? 'done' : 'active';
    },
  },
  components: { Todo },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
