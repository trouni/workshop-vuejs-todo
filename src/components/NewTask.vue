<template>
  <div class="task-card new-task">
    <div>
      <input
        v-model="title"
        @keypress.enter="$refs.descriptionInput.focus()"
        type="text"
        placeholder="What is your task?"
        ref="titleInput"
      />
      <textarea
        v-model="description"
        @keypress.enter="createTask(title, description)"
        placeholder="Add some details about your task..."
        ref="descriptionInput"
      ></textarea>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      title: "",
      description: "",
    };
  },

  mounted() {
    this.$refs.titleInput.focus();
  },

  methods: {
    createTask(title, description) {
      this.$emit("create-task", title, description);
    },
  },
};
</script>

<style lang="scss">
@keyframes expand-vertical {
  from {
    min-height: 0;
    height: 0;
  }
  to {
    min-height: 6rem;
  }
}

.new-task {
  animation: expand-vertical 0.2s;
  overflow: hidden;
  background-color: white;
  border-left: solid 5px #35495e;
  &,
  &:hover {
    transform: scale(1.1);
    box-shadow: 2px 3px 10px rgba(black, 0.2);
  }
  & + .tasks-list {
    pointer-events: none;
  }
  input {
    font-size: 1.17rem;
    font-weight: bold;
    width: 100%;
  }
  textarea {
    width: 100%;
    font-size: 0.9rem;
    resize: none;
  }
}
</style>
