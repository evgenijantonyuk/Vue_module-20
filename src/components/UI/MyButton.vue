<template>
  <el-button class="my-button">
    <slot></slot>
  </el-button>
</template>

<script>
export default {
  name: "MyButton"
}
</script>

<style scoped>
.my-button {
  margin: 0;
}
</style>