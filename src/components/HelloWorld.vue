<script>
  let id = 0
  
export default { 
  
  data() {
    return {
      titleClass: 'title',
      message: 'Hello World!',
      awesome: true,
      count: 0,
      text: '',
      counter: {
        count: 0
      },
      newTodo: '',
      hideCompleted: false,
      todos: [
        { id: id++, text: 'Learn HTML' },
        { id: id++, text: 'Learn JavaScript' },
        { id: id++, text: 'Learn Vue' }
      ],
      todoId: 1,
      todoData: null
    }
  },  
  computed: {
    filteredTodos() {
      return this.hideCompleted
        ? this.todos.filter((t) => !t.done)
        : this.todos
    }
  },
  methods: {
    increment() {
      this.count++
    },
    toggle() {
      this.awesome = !this.awesome
    },
    addTodo() {
      this.todos.push({ id: id++, text: this.newTodo })
      this.newTodo = ''
    },
    removeTodo(todo) {
      this.todos = this.todos.filter((t) => t !== todo)
    },
    async fetchData() {
      this.todoData = null
      const res = await fetch(
        `https://jsonplaceholder.typicode.com/todos/${this.todoId}`
      )
      this.todoData = await res.json()
    }
  },
  mounted() {
    this.$refs.p.textContent = 'mounted!',
    this.fetchData()
  },
  watch: {
    todoId() {
      this.fetchData()
    }
  }
  
}
</script>

<template>
  <!-- <h2>{{ msg || 'No props passed yet' }}</h2> -->
  <h1 v-bind:class="titleClass"> {{ message }}</h1>
  <p>Count is: {{ counter.count }}</p>
  <button @click="increment">count is: {{ count }}</button>
  <br><br><br>
  <H2>Form binding:</H2>
  <input v-model="text" placeholder="Type here">
  <p>Testo digitato: {{ text }}</p>
  <br><br><br>
  <h2>Conditional rendering</h2>
  <button @click="toggle">toggle</button>
  <h1 v-if="awesome">Vue is awesome!</h1>
  <h1 v-else>Oh no 😢</h1>
  <br><br><br>
  <h2>List rendering</h2>
  <form @submit.prevent="addTodo">
    <input v-model="newTodo">
    <button>Add Todo</button>    
  </form>
  <ul>
    <li v-for="todo in todos" :key="todo.id">
      {{ todo.text }}
      <button @click="removeTodo(todo)">X</button>
    </li>
  </ul>
  <br><br><br>

  <h2>Computed property</h2>
  <form @submit.prevent="addTodo">
    <input v-model="newTodo">
    <button>Add Todo</button>
  </form>
  <ul>
    <li v-for="todo in filteredTodos" :key="todo.id">
      <input type="checkbox" v-model="todo.done">
      <span :class="{ done: todo.done }">{{ todo.text }}</span>
      <button @click="removeTodo(todo)">X</button>
    </li>
  </ul>
  <button @click="hideCompleted = !hideCompleted">
    {{ hideCompleted ? 'Show all' : 'Hide completed' }}
  </button>  
  <br><br><br>

  <h2>Lifecycle and Template Refs</h2>
  <p ref="p">hello</p>

  <br><br><br>
  <h2>Watchers</h2>
  <p>Todo id: {{ todoId }}</p>
  <button @click="todoId++">Fetch next todo</button>
  <p v-if="!todoData">Loading...</p>
  <pre v-else>{{ todoData }}</pre>

</template>

<style>
.title {
  color: red;
}

.done {
  text-decoration: line-through;
  color: green;
}

</style>