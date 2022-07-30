<template>
  <div class="container">
    <h2>To-do List</h2>
    <form
      class="d-flex"
      @submit.prevent="onSubmit"
    >
      <div class="flex-grow-1 mr-2">
        <input
          v-model="todo"
          class="form-control"
          type="text"
          placeholder="Type new to-do"
        >
      </div>
      <div>
        <button 
          class="btn btn-primary"
          type="submit"
        >
          Add
        </button>
      </div>
    </form>
    {{ todoList }}
  </div>
</template>

<script>
import {ref} from 'vue';    // import

export default{
  setup(){
    const todo = ref('');
    const todoList = ref([]);

    const onSubmit = () => {
      //e.preventDefault();   // 자동 refresh 방지
      todoList.value.push({
        id: Date.now(),
        subject: todo.value
      });
    };

    return {
      todo,
      todoList,
      onSubmit
    }
  }
}
</script>

<style>
  .red{
    color:red;
  }
  .blue{
    color:blue;
  }
</style>
