<template>
  <div class="task-list">
    <div class="task-list-container">
      <transition-group name="task-list">
        <template v-for="task in tasks">
          <task-item
              v-if="task && !task.isEditing"
              :task="task"
              :key="task.task_id"
              @delete="$emit('delete', task)"
              @edit="$emit('edit', task)"
              @is-completed="$emit('is-completed', task)"
          />
          <task-form
              v-else-if="task"
              :task="task"
              :key="task.task_id"
              @completeEdit="$emit('completeEdit', task)"
          />
        </template>
      </transition-group>
    </div>
    <h2 class="empty-list" v-if="tasks.length===0">Список задач пуст...<br/>Добавьте новую!</h2>
  </div>

</template>

<script>
import TaskItem from "@/components/TaskItem";
import TaskForm from "@/components/TaskForm";

export default {
  name: "TaskList",
  components: {TaskForm, TaskItem},
  props: {
    tasks: {
      type: Array,
      required: true
    }
  },
  watch() {}
}
</script>

<style scoped>
.task-list {
  width: 100%;
}

.task-list-container {
  display: flex;
  align-items: center;
  flex-direction: column;
}

h2 {
  display: flex;
  text-align: center;
  justify-content: center;
  align-items: center;
  height: 100%;
}

.tasks-list-item {
  display: inline-block;
  margin-right: 10px;
}

.tasks-list-enter-active,
.tasks-list-leave-active {
  transition: all 1s ease;
}

.tasks-list-enter-from,
.tasks-list-leave-to {
  opacity: 0;
  transform: translateY(30px);
}

.tasks-list-move {
  transition: transform 0.5s ease;
}
</style>
