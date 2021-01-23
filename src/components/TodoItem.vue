<template>
  <li>
    <!--
      v-bind:class="{done: todo.completed} похоже на
      classname({ done: todo.completed })
    -->
    <span v-bind:class="{done: todo.completed}">
      <label>
        <!--
          v-on:change - событие
          v-on:change="todo.completed = true" похоже на
          onClick={todo.completed = true}
        -->
        <input
          type="checkbox"
          v-on:change="todo.completed = !todo.completed"
        >
      </label>
      <strong>{{index + 1}}</strong>
      &nbsp;
<!--      {{todo.title | uppercase}}-->
      {{todo.title}}
    </span>

    <!--
      v-on:click="$emit('remove-todo', todo.id)"
      Вызываем проброшенную коллбек функцию и передаём параметр
    -->
    <button
      class="rm"
      v-on:click="$emit('remove-todo', todo.id)"
    >&times;</button>
  </li>
</template>

<script>
export default {
  props: {
    // Пропсы, принимаемые компонетом, с указанием типов как в PropTypes
    todo: {
      type: Object,
      required: true
    },
    index: Number
  },
  filters: {
    uppercase(value) {
      return value.toUpperCase();
    }
  }
}
</script>

<style scoped>
  li {
    border: 1px solid #ccc;
    display: flex;
    justify-content: space-between;
    padding: .5rem .2rem;
    margin-bottom: 1rem;
  }

  .rm {
    background: red;
    color: #fff;
    border-radius: 50%;
    font-weight: bold;
  }

  .done {
    text-decoration: line-through;
  }
</style>
