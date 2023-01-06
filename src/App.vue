<script lang="ts">
// import HelloWorld from './components/HelloWorld.vue'

export default {
  data() {
    return {
      title: 'My To Do App',
      logoUrl: "https://upload.wikimedia.org/wikipedia/commons/6/67/Microsoft_To-Do_icon.png",
      logoCaption: "Todo App Logo",
      newTask: '',
      tasks: [
        { id: 1, name: 'Learn Vue JS', finished: 0 },
        { id: 2, name: 'Build a Vue application', finished: 0 },
        { id: 3, name: 'Write an article about Vue JS', finished: 0 }
      ]      
    }
  },
  methods: {
    addTask() {
      if (this.newTask.length < 1) {
        console.log(12);
      } else {
        this.tasks.push({
          id: this.tasks.length + 1,
          name: this.newTask,
          finished: 0
        });

        this.newTask = '' 
      }      
    },
    finishTask(task: any) {
      task.finished = 1;
    }
  },
  computed: {
    allTasks() {
        return this.tasks.length
    },
    latest() {
        return [...this.tasks].reverse()
    }
  }
}
</script>

<template>
  <img :src="logoUrl" :alt="logoCaption" height="100" width="100" />

  <h2 class="text-xl font-semibold">Add a new task</h2>

  <div class="flex">
    <input type="text"
        v-model="newTask"
        placeholder="Add a new task"
        class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
    >

    <button
      class="cursor-pointer"
      @click="addTask"
      :disabled="newTask.length < 1"
    >
      Add
    </button>
  </div>
  <p class="text-red-500 text-xs italic hidden" id="error">Please fill out this field.</p>

  <div v-if="newTask.length > 0">
    <h3>New task preview</h3>
    <p>{{ newTask }}</p>
  </div>

  <p class="text-xl font-semibold mt-5">{{ title }}</p>
  <ul class="mt-2">
    <li class="flex" v-for="task in tasks" :key="task.id">
      <p :class="{ 'line-through': task.finished }">
        {{ task.id }}. {{ task.name }}
      </p>      
      <a class="cursor-pointer mx-2" @click="finishTask(task)" :class="{ 'text-red-400': task.finished }">Finish Task</a>
      <a class="cursor-pointer">Delete Task</a>
    </li>
  </ul>

  <p class="mt-5">You have {{ allTasks }} {{ allTasks > 1 ? 'tasks' : 'task' }} at the moment</p>

</template>

<!--
<template>
  <HelloWorld msg="Vite + Vue" />
</template>
-->
