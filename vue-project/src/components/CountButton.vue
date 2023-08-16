<template>
    <div class="button_box">
      <button @click="incrementCount">Click me!</button>
      <p>Count: {{ count }}</p>
    </div>
</template>
  
<script setup>
import { ref } from 'vue';
  const count = ref(0);

  const incrementCount = () => {
    count.value++;
    console.log(count.value);
  };
</script>


<style>
  .button_box {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    height: 100vh;
  }

  button {
    background-color: #000;
    color: #fff;
    border: none;
    padding: 10px 20px;
    border-radius: 5px;
    cursor: pointer;
  }
</style>
  