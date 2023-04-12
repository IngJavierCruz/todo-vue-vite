<template>
  <h4 class="display-4 text-center">Tasks</h4>
  <form class="card tasks" @submit.prevent="saveTask($event)">
    <div class="mb-3">
      <label for="title" class="form-label">Title</label>
      <input
        type="title"
        class="form-control"
        id="title"
        placeholder="New Task"
        v-model="task.title"
      />
    </div>
    <div class="mb-3">
      <label for="description" class="form-label">Description</label>
      <textarea
        class="form-control"
        id="description"
        rows="3"
        placeholder="This is new task"
        v-model="task.description"
      ></textarea>
    </div>

    <div class="mb-3 m-auto">
      <button type="submit" class="btn btn-primary">Save</button>
    </div>
  </form>
  <hr />
  <div class="tasks">
    <h3 v-if="tasks.length === 0">Not found tasks</h3>
    <Task
      v-for="task in tasks"
      :task="task"
      :key="task.id"
      @remove="remove($event)"
      @complete="complete($event)"
      @incomplete="incomplete($event)"
    />
  </div>
</template>

<script>
import Task from "./Task.vue";
export default {
  name: "tasks",
  components: {
    Task,
  },
  data: () => ({
    task: {
      title: "Tarea 2",
      description: "Esta es una tarea 2",
      state: false,
    },
    tasks: [
      {
        id: 1,
        title: "Tarea 1",
        description: "Esta es una tarea",
        state: true,
      },
    ],
  }),
  methods: {
    saveTask() {
      const newTask = {
        ...this.task,
        id: new Date().getTime(),
        state: false,
      };
      this.tasks = [...this.tasks, newTask];
      this.task = {
        title: "",
        description: "",
        state: false,
      };
    },
    remove(id) {
      this.tasks = this.tasks.filter(x => x.id !== id);
    },
    complete(taskId) {
      this.tasks = this.tasks.map(x => x.id === taskId ? {...x, state: true} : x)
    },
    incomplete(taskId) {
      this.tasks = this.tasks.map(x => x.id === taskId ? {...x, state: false} : x)
    },
  },
};
</script>


<style scoped>
.tasks {
  width: 100%;
  padding: 1rem;
}
</style>
