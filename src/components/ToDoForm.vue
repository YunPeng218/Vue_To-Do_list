<template>
  <form @submit.prevent="onSubmit">
    <h2 class="label-wrapper">
      <label for="new-todo-input" class="label__lg">
        What needs to be done?
      </label>
    </h2>
    <input
      type="text"
      id="new-todo-input"
      name="new-todo"
      v-model.lazy.trim="label"
      class="input__lg" />
      <label for="category">Please select a category:
        <select name="category" v-model="category">
          <option value="Personal">Personal</option>
          <option value="Work">Work</option>
          <option value="Home">Home</option>
          <option value="Shopping">Shopping</option>
        </select>
      </label>
    <button type="submit" class="btn btn__primary btn__lg">Add</button>
  </form>
</template>

<script>
export default {
  methods: {
    onSubmit() {
      if (this.label === "") {
        window.alert("Please enter a todo item.");
        return;
      }
      if (this.category === "") {
        window.alert("Please select a category.");
        return;
      }
      this.$emit("todo-added", this.label, this.category);
      this.label = "";
      this.category = "";
    },
  },
  data() {
    return {
      label: "",
      category: "",
    };
  },
};
</script>
