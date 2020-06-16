<template>
  <div class="new-task">
    <input
      @keydown.enter="add"
      v-model="name"
      type="text"
      class="form-element"
      placeholder="Nova tarefa?"
    />
    <button class="form-element" @click="add">+</button>
  </div>
</template>

<script>
export default {
  data: () => ({
    name: ""
  }),

  methods: {
    add() {
      this.$emit("taskAdded", { name: this.name });
      this.name = "";
    }
  }
};
</script>

<style>
.new-task {
  margin: 35px;
}

.form-element {
  outline: none;
  font-size: 2rem;
  padding: 5px 10px 8px;
  border: 1px solid #fff;
  color: #fff;
}

input.form-element {
  width: 500px;
  background-color: #fff2;
  border-radius: 8px 0 0 8px;
}

button.form-element {
  border-left: none;
  background-color: #2196f3;
  border-radius: 0 8px 8px 0;
  transition: filter 0.15s;
}

button.form-element:hover {
  cursor: pointer;
  filter: brightness(0.9);
}
</style>