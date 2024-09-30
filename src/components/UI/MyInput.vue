<template>
  <el-input :model-value="modelValue" @update:model-value="updateInput" type="text" />
</template>

<script>
export default {
  name: "MyInput",
  props: {
    modelValue: [String, Number]
  },
  methods: {
    updateInput(value) {
      this.$emit('update:modelValue', value)
    }
  }
}
</script>

<style scoped>
</style>
