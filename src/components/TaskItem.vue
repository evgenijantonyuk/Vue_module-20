<template>
  <div :class="{ 'task-active': isCompleted }" class="task">
    <div class="task-content">
      <p :class="{ 'task-body-active': isCompleted }" class="task-body">{{ task.task_body }}</p>

      <p v-if="isCompleted" class="task-done"> - Выполнено</p>
    </div>
    <div class="task-btns">
      <el-checkbox class="check-box" v-model="isCompleted" @change="changeIsCompleted" size="large" />
      <Edit @click="$emit('edit', task)" class="edit-icon"/>
      <Delete @click="$emit('delete', task)" class="del-icon"/>
    </div>
  </div>
</template>

<script>
import MyButton from "@/components/UI/MyButton"
import { Delete, Edit } from "@element-plus/icons-vue"

export default {
  name: "TaskItem",
  components: { Delete, Edit, MyButton },
  props: {
    task: {
      type: Object,
      required: true
    }
  },
  data() {
    return {
      isCompleted: false,
      pClass: 'task-body'
    }
  },
  methods: {
    changeIsCompleted() {
      if(this.task) {
        this.task.isCompleted = this.isCompleted
        this.pClass += '-active'
      }
      this.$emit('is-completed', this.task)
    }
  }
}
</script>

<style scoped>
.task {
  background: #c6e2ff;
  height: 20%;
  width: 70%;
  padding: 1.5%;
  display: flex;
  justify-content: space-between;
  align-items: center;
  border-radius: 5px;
  margin: 1% 0;
}

.task-active {
  background: #83ff8a;
  height: 20%;
  width: 70%;
  padding: 1.5%;
  display: flex;
  justify-content: space-between;
  align-items: center;
  border-radius: 5px;
  margin: 1% 0;
}

.task-content {
  width: 80%;
  display: flex;
  align-items: center;
}

.task-btns {
  display: flex;
  justify-content: space-between;
  width: 13%;
  align-items: center;
}

.task-body {
  margin-right: 1%;
}

.task-body-active {
  margin-right: 1%;
  color: #77e377;
}

.task-done {
  margin-left: 1%;
  text-align: center;
  color: #65d965;
  text-decoration: line-through;
}

.task-content {
  display: flex;
  align-items: center;
}

.edit-icon {
  width: 1.5em;
  height: 1.3em;
  cursor: pointer;
  margin-right: 10px;
}

.del-icon {
  width: 1.5em;
  height: 1.3em;
  cursor: pointer;
}
</style>
