<template>
  <header class="header">
    <h1>Todo List</h1>
  </header>
</template>

<script>
export default {
  name: "Header"
};
</script>

<style lang="scss" scoped>
header {
  background: #333;
  color: white;
  text-align: center;
  padding: 10px;

  a {
    color: white;
    padding-right: 5px;
  }
}
</style>