<template>
  <div id="app">
    <!-- 229990343舒爽 -->
    <h1>任务清单</h1>
    <input v-model="newTask" placeholder="添加新任务">
    <button @click="addTask">添加任务</button>
    <ul>
      <li v-for="(task, index) in tasks" :key="index">
        <span :class="{ completed: task.completed }">
          {{ task.name }}
        </span>
        <input type="checkbox" v-model="task.completed">
        <span>{{ task.completed ? '已完成' : '未完成' }}</span>
        <button @click="editTask(index)">编辑</button>
        <button @click="deleteTask(index)">删除</button>
      </li>
    </ul>
    <button @click="clearTasks">清空所有任务</button>
  </div>
</template>

<script setup>
import { ref } from 'vue';

const tasks = ref([
  { name: '完成数学作业', completed: false },
  { name: '阅读一本小说', completed: true },
  { name: '练习绘画', completed: false }
]);
const newTask = ref('');

const addTask = () => {
  if (newTask.value.trim()) {
    tasks.value.push({ name: newTask.value, completed: false });
    newTask.value = '';
  }
};

const editTask = (index) => {
  const newName = prompt('请输入新的任务名称', tasks.value[index].name);
  if (newName !== null && newName.trim()) {
    tasks.value[index].name = newName;
  }
};
const deleteTask = (index) => {
  tasks.value.splice(index, 1);
};

const clearTasks = () => {
  tasks.value = [];
};
</script>

<style scoped>
.completed {
  text-decoration: line-through;
  color: #999;
}
</style>