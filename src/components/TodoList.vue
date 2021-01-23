<template>
  <div>
    <ul>
      <!--
        v-for - итерация по массиву, похоже на todos.map(todo => <TodoItem todo={todo} />)
        v-bind:todo - прокидываем пропс todo
        v-on:remove-todo - проброшенная в пропсы коллбек функция
      -->
      <TodoItem
        v-for="(todo, i) of todos"
        v-bind:todo="todo"
        v-bind:index="i"
        v-on:remove-todo="removeTodo"
      />
    </ul>
  </div>
</template>

<script>
import TodoItem from '@/components/TodoItem';
export default {
  // Пропсы, принимаемые компонетом
  props: ['todos'],
  // Регистрация импортируемых других компонентов для использования
  components: {
    TodoItem
  },
  methods: {
    // Методы, доступные в компоненте
    removeTodo(id) {
      this.$emit('remove-todo', id);
    }
  }
}
</script>

<!--
  scoped - стили применяются только внутри этого компонента
-->
<style scoped>
  ul {
    list-style: none;
    margin: 0;
    padding: 0;
  }
</style>

