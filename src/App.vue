<template>
  <div class="container">
    <h2>To-do List</h2>
    <form
      @submit.prevent="onSubmit"
    >
      <div class="d-flex">
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
      </div>

      <div
        v-show="hasError"
        style="color: red"
      >
        This field cannot be empty.
      </div>
    </form>
    <div 
      v-for="item in todoList"
      :key="item.id"
      class="card mt-2"
    >
      <div class="card-body p-2">
        {{ item.subject }}
      </div>
    </div>
  </div>
</template>

<script>
import {ref} from 'vue';

export default{
  setup(){
    const hasError = ref(false);
    const todo = ref('');
    const todoList = ref([
      {id: 1, subject: '휴대폰 사기'},
      {id: 2, subject: '장보기'},
    ]);

    const onSubmit = () => {
      if (todo.value === ''){
        hasError.value = true;
      } else {
        todoList.value.push({
        id: Date.now(),
        subject: todo.value
      });
        hasError.value=false;
        todo.value = '';
      }      
    };

    return {
      todo,
      todoList,
      onSubmit,
      hasError,
    };
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
