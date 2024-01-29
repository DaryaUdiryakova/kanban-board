<script>
export default {
  data() {
    return {
      newTask: "",
    };
  },
  methods: {
    save() {
      this.$emit("add", this.newTask);
      this.newTask = "";
    },
  },
};
</script>
<template>
  <div class="form-add">
    <h3>New Task</h3>
    <div class="form-add__input-group">
      <input v-model="newTask">
      <button
        class="button-add"
        @click="save"
        :disabled="!newTask"
      >
        Save
      </button>
    </div>
  </div>
</template>