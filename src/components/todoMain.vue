<template>
    <body>
        <main id="app">
            <section class="todo-list">
                <h3>To-do List</h3>
                <div v-if="todoList" class="all-todos">
                    <div
                        v-for="todo in todoList"
                        :key="todo.text"
                        class="single-todo"
                        :class="{ done: todo.done }"
                    >
                        <p>{{ todo.text }}</p>
                    </div>
                    <button class="clear" @click="clearAllTodos">Clear All</button>
                </div>
                <div v-else class="all-todos">Nothing todo</div>

                <label for="todoAdd">
                    <input
                        type="text"
                        placeholder="Add new todo"
                        id="todoAdd"
                        v-model="newTodo"
                        ref="todoAdd"
                    >
                </label>
                <button v-if="newTodo" class="add-active" @click="addTodo">Add</button>
                <button v-else class="add-inactive">Add</button>
                <div class="instructions">
                    Instructions:
                    <ul>
                        <li>Click the to-do text to toggle between done / undone</li>
                        <li>Use clear all button to remove all items</li>
                        <li>Use the input field to add new to-dos</li>
                    </ul>
                </div>
            </section>
        </main>
    </body>
</template>

<script>

export default {
  name: 'todoMain',
  components: {
    // TODO create todo item componeent
  },
  data() {
    return {
      newTodo: '',
      todoList: [],
    };
  },
  computed: {
    loadTodoList() {
      return JSON.parse(window.localStorage.getItem('todoList'));
    },
  },
  mounted() {
    this.todoList = this.loadTodoList ? this.loadTodoList : [];
  },
  methods: {
    addTodo() {
      const todo = {
        text: this.$refs.todoAdd.value,
        done: false,
      };
      this.todoList.push(todo);
      localStorage.setItem('todoList', JSON.stringify(this.todoList));
    },
    clearAllTodos() {
      this.todoList = [];
      localStorage.setItem('todoList', JSON.stringify(this.todoList));
    },
  },
};
</script>

<style>
@import '../assets/css/style.css';
</style>
