<template>
    <body>
        <main id="app">
            <section class="todo-list">
                <h3>To-do List</h3>
                <div v-if="todoList.length > 0" class="all-todos">
                    <div
                        v-for="todo in todoList"
                        :key="todo.id"
                        class="single-todo"
                        :class="{ done: todo.done }"
                    >
                        <p>{{ todo.text }}</p>
                        <button
                            v-if="todo.done"
                            class="delete"
                            @click="deleteTodo(todo)">
                        </button>
                        <button
                            v-else class="done"
                            @click="doneTodo(todo)">
                        </button>
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
    this.$refs.todoAdd.focus();
  },
  methods: {
    updateLocalStorage(data) {
      localStorage.setItem('todoList', JSON.stringify(data));
    },
    addTodo() {
      console.log(this.todoList.length);
      const todo = {
        text: this.$refs.todoAdd.value,
        done: false,
        id: this.todoList.length === 0 ? 1 : this.todoList[this.todoList.length - 1].id + 1,
      };
      this.todoList.push(todo);
      this.updateLocalStorage(this.todoList);
      this.newTodo = '';
      this.$refs.todoAdd.focus();
    },
    clearAllTodos() {
      this.todoList = [];
      this.updateLocalStorage(this.todoList);
    },
    doneTodo(data) {
      this.todoList.forEach((todo, index) => {
        if (todo.id === data.id) {
          this.todoList[index].done = true;
        }
      });
      this.updateLocalStorage(this.todoList);
    },
    deleteTodo(data) {
      this.todoList = this.todoList.filter((todo) => todo.id !== data.id);
      this.updateLocalStorage(this.todoList);
    },
  },
};
</script>

<style>
@import '../assets/css/style.css';
</style>
