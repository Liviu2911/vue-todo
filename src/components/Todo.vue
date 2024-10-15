<script lang="ts">
import { TrashIcon } from "@heroicons/vue/16/solid";

export default {
  props: {
    todo: {
      type: Object,
      required: true,
    },
  },
  data(props) {
    return {
      props,
    };
  },
  methods: {
    changeStatus() {
      this.$emit(
        "changeStatus",
        this.todo.status === "done" ? "" : "done",
        this.todo.id
      );
    },
    deleteTodo() {
      this.$emit("deleteTodo", this.todo.id);
    },
    setActiveTodo() {
      this.$emit("setActiveTodo", this.todo);
    },
  },
  components: {
    TrashIcon,
  },
};
</script>

<template>
  <div
    class="px-4 py-2.5 rounded border flex flex-row justify-between gap-16 items-center transition-all"
    :class="
      props.todo.status === 'done' ? 'border-green-500' : 'border-slate-200'
    "
  >
    <button @click="setActiveTodo" class="w-40 text-start">
      {{
        props.todo.name.length > 15
          ? props.todo.name.slice(0, 15) + "..."
          : props.todo.name
      }}
    </button>
    <div class="flex flex-row gap-2 items-center">
      <button @click="deleteTodo()" class="hover:text-rose-500 transition-all">
        <TrashIcon class="size-5" />
      </button>
      <button
        @click="changeStatus"
        :class="
          props.todo.status !== 'done'
            ? 'p-2 border border-slate-200 rounded hover:bg-green-500 transition-all'
            : 'bg-green-500 p-2 rounded border'
        "
      ></button>
    </div>
  </div>
</template>
