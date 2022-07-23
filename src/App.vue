<template>
  <div :class="color">
    <!-- v-bind: 와 : 는 동일-->
    {{ name }}    <!-- {{ object }} 형식으로 사용 -->
  </div>
  <input
    :type="typeName"
    :value="name"
  >     <!-- name 과 bidning -->
  <button 
    class="btn btn-primary"
    @click="updateName"
  >
    <!-- v-on: 과 @ 는 동일 -->
    Click
  </button>
</template>

<script>
import {ref} from 'vue';    // import

export default{
  setup(){
    const name = ref('cointreau');    // ref로 감싸줌
    const typeName = ref('number');
    const color = ref('red');

    const updateName = () => {
      name.value = 'coder';    // .value 를 사용해서 변경
      typeName.value = 'text';
      color.value = 'blue';
    };

    // object return, template 안에서 접근 가능해짐
    return {
      name,
      updateName,
      typeName,
      color
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
