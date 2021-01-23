<template>
  <h2>Todo List</h2>
  <router-link to="/">Home</router-link>
  <hr />
  <AddTodo
      @add-todo="addTodo"
  />

  <select v-model="filter">
    <option value="all">All</option>
    <option value="completed">Completed</option>
    <option value="not-completed">Not Completed</option>
  </select>

  <!--
    v-if = условие, если false, компонент не показывается
  -->
  <Loader v-if="loading"/>
  <!--
    v-bind:todo - передача пропса
    @ - заменяет v-on
    v-else-if = дополнение условия
  -->
  <TodoList
      v-else-if="filteredTodos.length"
      v-bind:todos="filteredTodos"
      @remove-todo="removeTodo"
  />
  <!--
    v-else = дополнение условия, иначе
  -->
  <p v-else>No todos!</p>
</template>

<script>
import TodoList from '@/components/TodoList';
import AddTodo from '@/components/AddTodo';
import Loader from '@/components/Loader';
export default {
  name: 'App',
  // Стейт
  data() {
    return {
      todos: [],
      loading: true,
      filter: 'all'
    }
  },
  // Хуки жизненного цикла
  // mounted - то же что и componentDidMount
  mounted() {
    fetch('https://jsonplaceholder.typicode.com/todos?_limit=3')
        .then(response => response.json())
        .then(json => {
          setTimeout(() => {
            this.todos = json
            this.loading = false;
          }, 1000);
        });
  },
  // watch: {
  //   filter(value) {
  //     console.log(value);
  //   }
  // },

  computed: {
    filteredTodos() {
      if (this.filter === 'all') {
        return this.todos;
      }

      if (this.filter === 'completed') {
        return this.todos.filter(t => t.completed);
      }

      if (this.filter === 'not-completed') {
        return this.todos.filter(t => !t.completed);
      }
    }
  },

  // Методы в текущем компоненте
  methods: {
    removeTodo(id) {
      this.todos = this.todos.filter(item => item.id !== id);
    },
    addTodo(todo) {
      this.todos.push(todo);
    }
  },
  // Используемые в шаблоне компоненты
  components: {
    TodoList,
    AddTodo,
    Loader
  }
}
</script>
