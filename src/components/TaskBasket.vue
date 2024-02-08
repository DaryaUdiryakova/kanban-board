<script>
export default {
  props: {
    disabledButton: Number,
  },
  methods: {
    remove() {
      this.$emit("remove");
    },
  },
};
</script>

<template>
  <div class="task-basket">
    <button
      class="button-delete "
      @click="remove"
      :disabled="!disabledButton"
    >
      Delete
    </button>
  </div>
</template>