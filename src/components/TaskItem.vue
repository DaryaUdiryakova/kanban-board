<script>
export default {
  data() {
    return {
      isEdit: false,
      newName: this.name,
    };
  },
  props: {
    name: String,
    id: Number,
  },
  emits: ["change", "removeOne"],
  methods: {
    save() {
      this.isEdit = false;
      this.$emit("change", this.id, this.newName);
    },

    edit() {
      this.isEdit = true;
    },

    removeOne() {
      this.$emit("removeOne", this.id);
    },
  },
  directives: {
    focus: {
      mounted(el) {
        el.focus();
      },
    },
  },
};
</script>

<template>
  <div class="list__item">
    <template v-if="!isEdit">
      {{ name }}
      <button
        class="button-edit-save icon-actions"
        @click="edit"
      >
        <i
          class="fa fa-pencil"
          aria-hidden="true"
        ></i>
      </button>
    </template>
    <template v-else>
      <input
        class="input-edit"
        v-model="newName"
        v-focus
        draggable="false"
      >
      <button
        class="button-edit-save icon-actions"
        @click="save"
        v-if="newName"
      >
        <i
          class="fa fa-check"
          aria-hidden="true"
        ></i>
      </button>
      <button
        class="button-edit-save icon-actions"
        @click="removeOne"
        v-else
      >
        <i
          class="fa fa-trash"
          aria-hidden="true"
        ></i>
      </button>
    </template>
  </div>
</template>