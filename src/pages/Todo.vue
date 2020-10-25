<template>
  <q-page class="bg-grey-3 column">
    <q-list class="bg-white" separator>
      <q-item
        v-for="{ task, index } in tasks"
        :key="task.title"
        class=""
        clickable
        @click="task.done = !task.done"
        :class="{ done: task.done }"
      >
        <q-item-section avatar>
          <q-checkbox
            v-model="task.done"
            color="primary"
            class="no-pointer-events"
          />
        </q-item-section>
        <q-item-section>
          <q-item-label>{{ task.title }}</q-item-label>
        </q-item-section>
        <q-item-section v-if="task.done" side>
          <q-btn
            round
            dense
            unelevated
            color="primary"
            icon="delete"
            @click.stop="deleteTaskWithConfirmation(index)"
          />
        </q-item-section>
      </q-item>
    </q-list>
  </q-page>
</template>

<script>
export default {
  data() {
    return {
      tasks: [
        {
          title: "task",
          done: false,
        },
        {
          title: "task",
          done: false,
        },
        {
          title: "task",
          done: false,
        },
      ],
    };
  },

  methods: {
    deleteTaskWithConfirmation(index) {
      this.$q
        .dialog({
          title: "Confirm",
          message: "Delete Task?",
          cancel: true,
          persistent: true,
        })
        .onOk(() => {
          this.tasks.splice(index, 1);
          this.$q.notify("Task removed successfully.");
        });
    },
    deleteTask(index) {
      this.tasks.splice(index, 1);
      this.$q.notify("Task removed successfully.");
    },
  },
};
</script>

<style lang="scss">
.done {
  .q-item__label {
    text-decoration: line-through;
    color: #9c9c9c;
  }
}
</style>
