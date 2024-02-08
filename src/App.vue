<script>
import draggable from "vuedraggable";
import TaskItem from "@/components/TaskItem.vue";
import TaskFormAdd from "@/components/TaskFormAdd.vue";
import TaskBasket from "@/components/TaskBasket.vue";

let idTask = 6;
export default {
  components: {
    draggable,
    TaskFormAdd,
    TaskItem,
    TaskBasket,
  },
  data() {
    return {
      board: [
        {
          id: 0,
          title: "Backlog",
          style: "list-bg-backlog",
          tasks: [
            { id: 0, name: "Add new category" },
            { id: 1, name: "Make payment modal more visible" },
            { id: 2, name: "Add new illustrations" },
            { id: 3, name: "Create newsletter template" },
          ],
        },
        {
          id: 1,
          title: "In Progress",
          style: "list-bg-progress",
          tasks: [{ id: 4, name: "Upload user avatars" }],
        },
        {
          id: 2,
          title: "Done",
          style: "list-bg-done",
          tasks: [
            { id: 5, name: "Content edits" },
            { id: 6, name: "Redesign website" },
          ],
        },
        {
          id: 3,
          title: "Basket",
          style: "list-bg-basket",
          tasks: [],
        },
      ],
    };
  },
  methods: {
    addTask(title) {
      idTask++;
      this.board[0].tasks.push({ id: idTask, name: title });
    },

    remove() {
      this.board[3].tasks = [];
    },

    change(id, name) {
      this.board = this.board.map((item) => {
        item.tasks.map((i) => {
          if (i.id === id) {
            i.name = name;
          }
          return i;
        });
        return item;
      });
    },
    removeOne(id) {
      this.board = this.board.map((item) => {
        item.tasks = item.tasks.filter((i) => {
          return i.id !== id;
        });
        return item;
      });
    },
  },
  computed: {
    dragOptions() {
      return {
        animation: 250,
      };
    },
  },
};
</script>

<template>
  <div class="wrapper">
    <header>
      <div class="container">
        <task-form-add @add="addTask" />
      </div>
    </header>
    <main>
      <div class="container">
        <div
          class="list"
          v-for="item in board"
          :class="item.style"
          :key="item.id"
        >
          <h3>{{item.title}}</h3>
          <draggable
            :class="{ 'list-zero': !item.tasks.length }"
            class="list__group"
            :list="item.tasks"
            group="task"
            itemKey="id"
            v-bind="dragOptions"
          >
            <template #item="{element}">
              <task-item
                :name="element.name"
                :id="element.id"
                @change="change"
                @removeOne="removeOne"
              >
              </task-item>
            </template>
          </draggable>
          <task-basket
            v-if="item.title === 'Basket'"
            @remove="remove"
            :disabledButton="item.tasks.length"
          ></task-basket>
        </div>
      </div>
    </main>
  </div>
</template>
