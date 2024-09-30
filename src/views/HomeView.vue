<template>
  <div class="home">
    <div class="task-wrapper">
      <h1>Задачи к выполнению</h1>
      <el-container class="el-container">
        <el-header class="header">
          <task-form v-if="!searchMark" @create="createTask" class="el-form"/>
          <el-input v-model="searchBody" placeholder="Найти Задачу" style="width: 50%;" v-if="searchMark"/>
          <Search class="search-icon" @click="searchMark=!searchMark" />
        </el-header>
        <el-main class="main">
          <el-scrollbar height="25em">
            <task-list
                :tasks="searchedTasks"
                @delete="delTask"
                @edit="editTask"
                @completeEdit="editFormTask"
                @is-completed="completeTask"/>
          </el-scrollbar>
          <div class="count-container">
            <p>количество задач: <strong>{{ tasks.length }}</strong></p>
          </div>
        </el-main>
      </el-container>
    </div>
  </div>
</template>

<script>

import MyInput from "@/components/UI/MyInput";
import TaskForm from "@/components/TaskForm";
import MyButton from "@/components/UI/MyButton";
import TaskList from "@/components/TaskList";
import axios from "axios";

export default {
  name: 'HomeView',
  components: {
    TaskList,
    MyButton,
    TaskForm,
    MyInput
  },

  data() {
    return {
      tasks: [],
      searchMark: false,
      searchBody: ''
    }
  },

  methods: {
    createTask(task_body) {
      const newTask = {
        task_id: Date.now(),
        task_body: task_body,
        isCompleted: false,
        isEditing: false
      }
      this.tasks.push(newTask)
      console.log(this.tasks)
      localStorage.setItem("tasks", JSON.stringify(this.tasks))
    },
    delTask(task) {
      this.tasks = this.tasks.filter(todo => todo.task_id !== task.task_id)
      localStorage.setItem("tasks", JSON.stringify(this.tasks))
    },
    editTask(task) {
      this.tasks = this.tasks.map(todo => todo.task_id === task.task_id ? {...todo, isEditing: !todo.isEditing} : todo)
      console.log(this.tasks)
    },
    editFormTask(task) {
      this.tasks = this.tasks.map(todo => todo.task_id === task.task_id ? {
        ...todo,
        isEditing: !todo.isEditing,
        task_body: task.task_body
      } : todo)
      console.log(this.tasks)
      console.log('edit task in editFormTask', task)
      localStorage.setItem("tasks", JSON.stringify(this.tasks))
    },
    completeTask(task) {
      this.tasks = this.tasks.map(todo => todo.task_id === task.task_id ? {
        ...todo,
        isCompleted: !todo.isCompleted
      } : todo)
    },
    async fetchTasks() {
      try {
        const response = await axios.get('http://localhost:3000/tasks')
        this.tasks = response.data

      } catch (e) {}
    }
  },
  async mounted() {
    const data = localStorage.getItem('tasks')
    if (data) {
      this.tasks = JSON.parse(data)
    }

    await this.fetchTasks()
  },
  computed: {
    searchedTasks() {
      return this.tasks.filter(todo => todo.task_body.toLowerCase().includes(this.searchBody.toLowerCase()))
    }
  }
}
</script>

<style>

.task-wrapper {
  width: 50%;
  margin: 5% auto;
}

.el-container {
  border-radius: 10px;
}

header.header {
  display: flex;
  justify-content: center;
  align-items: center;
  background: #c6e2ff;

}

main.main {
  background: #ecf5ff;
  max-height: 30em;
  overflow-y: auto;
}

.count-container {
  margin: 0.7% auto;
}

.search-icon {
  width: 1.5em;
  height: 1.5em
}

</style>
