<template>
  <!--
    @ - замена v-on
    @submit.prevent - отправка
  -->
  <form @submit.prevent="onSubmit">
    <label>
      <!--
        v-model - это модель для инпута, заменяющая value и onChange
      -->
      <input type="text" v-model="title" />
    </label>
    <button type="submit">Create</button>
  </form>
</template>

<script>
export default {
  data() {
    // Обьект стейта компонента
    return {
      title: ''
    }
  },
  methods: {
    onSubmit() {
      if (this.title.trim()) {
        const newTodo = {
          id: Date.now(),
          title: this.title,
          completed: false
        }
        this.$emit('add-todo', newTodo);
        this.title = '';
      }
    }
  }
}
</script>

<style scoped>
  form {
    display: flex;
  }

  input {
    width: 400px;
  }
</style>
