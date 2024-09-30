<template>
  <form @submit.prevent class="form">
    <el-input v-model="task_body"
              type="text"
              placeholder="Новая задача"
              class="form-input"/>
    <my-button @click="createNewBody" class="add-btn">Добавить</my-button>
  </form>
</template>

<script>
import MyInput from "@/components/UI/MyInput"
import MyButton from "@/components/UI/MyButton"

export default {
  name: "TaskForm",
  components: { MyButton, MyInput },
  props: {
    task: {
      type: Object,
      required: false
    }
  },
  data() {
    return {
      task_body: this.task ? this.task.task_body : ''
    }
  },
  methods: {
    createNewBody() {
      if (this.task_body === '') return
      this.$emit('create', this.task_body)
      if(this.task) {
        this.task.task_body = this.task_body
      }
      this.task_body = ''
      this.$emit('completeEdit', this.task)
    }
  }
}
</script>

<style scoped>
.form {
  display: flex;
  width: 80%;
  justify-content: center;
}

.form-input {
  width: 65%;
  margin-right: 15px;
}

.add-btn {
  border: none;
  background-color: #66adf3;
  color: #fff;
  transition: all .3s ease-in-out;
}
</style>
