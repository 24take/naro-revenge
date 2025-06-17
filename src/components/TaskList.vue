<script setup lang="ts">
import { ref } from 'vue'

interface Task {
  title: string
  completed: boolean
}

const tasks = ref<Task[]>([
  { title: 'あ', completed: false },
  { title: 'い', completed: false },
  { title: 'う', completed: true }
])

const newTaskName = ref<string>('')
const addTask = () => {
  if (newTaskName.value === '') {
    alert('タスク名を入力してください。')
    return
  }
  tasks.value.push({ title: newTaskName.value, completed: false })
  newTaskName.value = ''
}
</script>

<template>
  <div>
    <div>未完了タスク一覧</div>
    <ul>
      <template v-for="task in tasks" :key="task.title">
        <li v-if="!task.completed">
          {{ task.title }}
          <button @click="task.completed = true">完了にする</button>
        </li></template
      >
    </ul>
    <div>完了済タスク一覧</div>
    <ul>
        <template v-for="task in tasks" :key="task.title">
        <li v-if="task.completed">
          {{ task.title }}
          <button @click="task.completed = false">未完了に戻す</button>
        </li>
        </template>
    </ul>
  </div>
  <div>
    <label>
        タスク
        <input v-model="newTaskName" type="text"/>
        <button @click="addTask">タスクを追加</button>
    </label>
  </div>
</template>
