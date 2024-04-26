<template>
  <form class="stack-small" @submit.prevent="onSubmit">
    <div>
      <label class="edit-label">Editing details for "{{ label }}" </label>
      <input
        :id="id"
        ref="labelInput"
        type="text"
        v-model.lazy.trim="editedLabel" />
      <label for="editedCategory">Please select a category:
        <select name="editedCategory" v-model="editedCategory">
          <option value="Personal">Personal</option>
          <option value="Work">Work</option>
          <option value="Home">Home</option>
          <option value="Shopping">Shopping</option>
        </select>
      </label>
    </div>
    <div class="btn-group">
      <button type="button" class="btn" @click="onCancel">
        Cancel
      </button>
      <button type="submit" class="btn btn__primary">
        Save
      </button>
    </div>
  </form>
</template>

<script>
export default {
  props: {
    label: {
      type: String,
      required: true,
    },
    category: {
      type: String,
      required: true,
    },
    id: {
      type: String,
      required: true,
    },
  },
  data() {
    return {
      editedLabel: this.label,
      editedCategory: this.category,
    };
  },
  methods: {
    onSubmit() {
      if (!this.editedLabel) {
        window.alert("Please do not leave the required field blank.");
        return;
      }
      if (this.editedLabel !== this.label || this.editedCategory !== this.category) {
        this.$emit("item-edited", {editedLabel: this.editedLabel, editedCategory: this.editedCategory});
      }
    },
    onCancel() {
      this.$emit("edit-cancelled");
    },
  },
};
</script>

<style scoped>
.edit-label {
  font-family: Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #0b0c0c;
  display: block;
  margin-bottom: 5px;
}
input {
  display: inline-block;
  margin-top: 0.4rem;
  width: 100%;
  min-height: 4.4rem;
  padding: 0.4rem 0.8rem;
  border: 2px solid #565656;
}
form {
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
}
form > * {
  flex: 0 0 100%;
}
</style>
