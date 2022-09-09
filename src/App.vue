<script setup>
  import TodoList from './components/TodoList.vue'
  </script>
  
<template>
    <header>
      <div>
        <todo-list></todo-list>
      </div>
      <div>  
      </div>
    </header>
  <body>
  </body>
</template>
  
<style>
  @import './assets/styles.css';
  * {
    box-sizing: border-box;
    margin: auto;
  }
  header {
    line-height: 1.5;
  }
  
  @media (min-width: 1024px) {
    body {
      display: flex;
      place-items: center;
    }
    
  }
</style>