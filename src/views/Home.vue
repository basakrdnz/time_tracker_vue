<template>
  <div class="home">
    <TaskForm @task-added="addTask" />
    <TaskList :tasks="tasks" @update-time="updateTime" @complete-task="completeTask" @delete-task="deleteTask" />
    <Report :totalTime="totalTime" />
  </div>
</template>

<script>
import TaskForm from '../components/TaskForm.vue';
import TaskList from '../components/TaskList.vue';
import Report from '../components/Report.vue';

export default {
  components: {TaskForm, TaskList, Report},
  data() {
    return {
      tasks: [],
      totalTime: 0,
    };
  },
  methods: {
    addTask(task) {
      this.tasks.push({...task, id: Date.now()});
    },
    updateTime({taskId, time}) {
      this.totalTime = this.tasks.reduce((sum, task) => sum + (task.timeSpent || 0), 0);
    },
    completeTask(task) {
      task.isCompleted = true;
      this.updateTime({taskId: task.id, time: task.timeSpent});
    },
    deleteTask(id) {
      this.tasks = this.tasks.filter((task) => task.id !== id);
      this.updateTime({taskId: null, time: 0});
    },
  },
};
</script>

<style>
.home {
  padding: 20px;
}
</style>
