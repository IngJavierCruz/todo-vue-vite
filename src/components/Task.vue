<template>
  <div class="card my-3">
    <div class="card-body">
    <div class="card-title">
      <i v-if="task.state" class="fas fa-check-circle cursor-pointer text-success" @click="complete(false)"></i>
      <i v-else class="far fa-circle cursor-pointer" @click="complete(true)"></i>
      Title: {{ task.title }}</div>
      <p class="card-text">Description: {{ task.description }}</p>
      <div class="buttons">
        <!-- <button type="button" class="btn btn-primary" @click="modify()">Modificar</button> -->
        <button type="button" class="btn btn-danger"  @click="remove()">Eliminar</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "task",
  props: {
    task: {
      required: true,
      type: Object,
    },
  },
  methods: {
    modify() {
      this.$emit('update', this.task)
    },
    remove() {
      this.$emit('remove', this.task.id)
    },
    complete(isComplete) {
      if (isComplete) {
        this.$emit('complete', this.task.id)
      } else {
        this.$emit('incomplete', this.task.id)
      }
    }
  }
};
</script>


<style lang="scss">
.buttons {
  display: flex;
  justify-content: center;

  & .btn:first-child {
    margin-right: 1rem;
  }
}

.cursor-pointer {
  cursor: pointer;
}
</style>

