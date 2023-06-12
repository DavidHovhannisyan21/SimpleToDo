<template>
  <div class="app">
    <main>
      <header>
        <img src="./assets/pinia-logo.svg" alt="pinia logo">
        <h1>Pinia Tasks</h1>
      </header>

      <div class="new-task-form">
        <TaskForm />
      </div>


      <nav class="filter">
        <button @click="filter = 'all'">All Tasks</button>
        <button @click="filter = 'favs'">Favorite Tasks</button>
      </nav>


      <div class="task-list" v-if="filter === 'all'">
        <p>You have {{ taskStore.totalCount }} tasks left to do</p>
        <div v-for="task in taskStore.tasks" :key="task">
          <task-details :task="task"/>
        </div>
      </div>

      <div class="task-list" v-if="filter === 'favs'">
        <p>You have {{ taskStore.favCount }} favs left to do</p>
        <div v-for="task in taskStore.favs" :key="task">
          <task-details :task="task"/>
        </div>
      </div>

    </main>
  </div>

</template>

<script>
  import { ref } from 'vue'
  import TaskDetails from './components/TaskDetails.vue'
  import { useTaskStore } from './stores/TaskStore'
  import TaskDetailsVue from './components/TaskDetails.vue'
  import TaskForm from './components/TaskForm.vue'
  export default{
    setup(){
      const taskStore = useTaskStore()

      taskStore.getTasks()

      const filter = ref('all')
      return { taskStore,filter }
    },
    components:{
      TaskDetails,
      TaskForm
    }
  }
</script>

