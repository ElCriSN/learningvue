<script>
let id = 0 
export default {
  
  data() {

    return {
      todoId: 1,
      todoData: null,
      message: 'Hellow Worl =DDD!',
    
        count: 0
  ,
      titleClass: 'title',
      text: '',
      awesome: true,
      newTodo: '',
      hideCompleted: false,
      todos: [
        {id: id++, text: 'LEARN HTEML =DD!', done: true},
        {id: id++, text: 'LEARN JAVASCRIPTTT =DDD!!', done: true},
        {id: id++, text: 'LEARN VUEEEJSSSS=DDD!!', done: false}
      ]
      
    }
  },
  computed: {
    filteredTodos(){
      return this.hideCompleted
        ? this.todos.filter((t)=> !t.done)
        : this.todos
    }
  },
  methods: {
    async fetchData() {
      this.todoData = null
      const res = await fetch (
        `https://jsonplaceholder.typicodecom/todos/${this.todoId}`
      )
      this.todoData = await res.json()
    },
    addTodo() {
      this.todos.push({ id: id++, text: this.newTodo})
      this.newTodo = ''
    },
    removeTodo(todo){ 
      this.todos = this.todos.filter((t)=> t!== todo)
    },
    increment() {
      this.count++
    },
    onInput(e){
      this.text = e.target.value
    },
    toggle() {
      this.awesome= !this.awesome
    }
  },
  mounted() {
    this.$refs.p.textContent = 'mounted!XP',
    this.fetchData
  },
  watch: {
    todoId() {
      this.fetchData()
    }
  }
}
</script>  
<script setup>

import { RouterLink, RouterView } from 'vue-router'

</script>

<template>

  <p>TOdo id: {{  todoId }}</p>
  <button @click="todoId++">FETHC NEXT TODOO =DD!</button>
  <p v-if="!todoData">Loadin'''XP</p>
  <pre v-else>{{ todoData }}</pre>
   <p ref="p">HELLLOW =DD!</p>
  <form @submit.prevent="addTodo">
    <input v-model="newTodo"/>
    <button>ADD TODOOO =DD!</button>
  </form>
  <ul>
    <li v-for="todo in filteredTodos" :key="todo.id">
      <input type="checkbox" v-model="todo.done"/>
      <span :class="{ done: todo.done }">{{ todo.text }}</span>
      <button @click="removeTodo(todo)">X</button>
    </li>
  </ul>
  <button @click="hideCompleted = !hideCompleted">
    {{ hideCompleted ? 'Show ALll =DD!' : 'Hide Completeeed =DDD!'}}
  </button>
  <button @click="toggle">toggle xP!</button>
  <h1 v-if="awesome">VUE IS AWESOMEEEEEEEE =p!!</h1>
 <h1 v-else>Oh noooo =)!!</h1> 
  <input v-model="text" placeholder="Type Here xP!!"/>
  <p>{{ text }}</p>
  <h1 :class="titleClass">Make me Red =)!!</h1>
  <h1>{{ message.split('').reverse().join('') }} 😀 !!</h1>
  <button @click="increment">COunt's : {{count }}</button>
  <header>
    <img alt="Vue logo" class="logo" src="@/assets/logo.svg" width="125" height="125" />

    <div class="wrapper">
      <HelloWorld msg="You did it!" />

      <nav>
        <RouterLink to="/">Home</RouterLink> |
        <RouterLink to="/about">About</RouterLink> |
        <a href="/about">A Tag About =P!</a>

      </nav>
    </div>
  </header>

  <RouterView />
</template>

<style scoped>
header {
  line-height: 1.5;
  max-height: 100vh;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

nav {
  width: 100%;
  font-size: 12px;
  text-align: center;
  margin-top: 2rem;
}

nav a.router-link-exact-active {
  color: var(--color-text);
}

nav a.router-link-exact-active:hover {
  background-color: transparent;
}

nav a {
  display: inline-block;
  padding: 0 1rem;
  border-left: 1px solid var(--color-border);
}

nav a:first-of-type {
  border: 0;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }

  nav {
    text-align: left;
    margin-left: -1rem;
    font-size: 1rem;

    padding: 1rem 0;
    margin-top: 1rem;
  }
}

.title {
  color: red;
}

.done {
  text-decoration: line-through;
}
</style>
