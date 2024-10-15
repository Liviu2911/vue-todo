<script>
export default {
  data() {
    return {
      value: "",
    };
  },
  methods: {
    addTodo() {
      this.$emit("addTodo", this.value);
      this.value = "";
    },
    update(e) {
      this.value = e.target.value;
    },
  },
};
</script>

<template>
  <form @submit.prevent="addTodo" class="flex flex-col items-center gap-2">
    <input
      @change="update"
      :value="this.value"
      type="text"
      class="outline-none border border-slate-200 rounded px-4 py-2.5 focus:border-sky-500 transition-all"
    />
    <button type="submit">Create</button>
  </form>
</template>
