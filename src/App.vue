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
    <div v-if="(todoList.length==0)">
      추가된 Todo 가 없습니다.
    </div>
    <div 
      v-for="(item, idx) in todoList"
      :key="item.id"
      class="card mt-2"
    >
      <div class="card-body p-2 d-flex align-items-center">
        <div class="form-check flex-grow-1">
          <input 
            v-model="item.completed" 
            class="form-check-input"
            type="checkbox"
          >
          <label 
            class="form-check-label"
            :class="{ todo: item.completed }"
          >{{ item.subject }}</label>
        </div>
        <div>
          <button
            class="btn btn-danger btn-sm"
            @click="deleteTodo(idx)"
          >
            Delete
          </button>
        </div>
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
    const todoList = ref([]);
    const todoStyle = {
      textDecoration: 'line-through',
      color: 'grey'
    };

    const onSubmit = () => {
      if (todo.value === ''){
        hasError.value = true;
      } else {
        todoList.value.push({
        id: Date.now(),
        subject: todo.value,
        completed: false,
      });
        hasError.value=false;
        todo.value = '';
      }      
    };

    const deleteTodo = (i) => {
      todoList.value.splice(i, 1);
      console.log(todoList.value);
    };

    return {
      todo,
      todoList,
      onSubmit,
      hasError,
      todoStyle,
      deleteTodo
    };
  }
}
</script>

<style>
  .todo {
    color: grey;
    text-decoration: line-through;
  }
</style>
