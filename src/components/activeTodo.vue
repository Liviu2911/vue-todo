<script lang="ts">
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
    close() {
      this.$emit("close");
    },
  },
};
</script>

<template>
  <div
    class="w-full h-[100vh] absolute top-0 left-0 bg-black bg-opacity-30 z-20 flex items-center justify-center"
  >
    <div class="p-4 rounded bg-white flex flex-col gap-2 items-center">
      <h1>{{ props?.todo?.name }}</h1>
      <button @click="close" class="hover:text-rose-500 transition-all">
        Close
      </button>
    </div>
  </div>
</template>
