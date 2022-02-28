<template>
  <div class="dark:bg-gray-900 app-container">
    <div class="container items-center mx-auto p-5">
      <div class="flex justify-between">
        <h1 class="text-2xl dark:text-white font-bold uppercase">Invoices</h1>
        <button
          type="button"
          class="text-white bg-gradient-to-r from-blue-500 via-blue-600 to-blue-700 hover:bg-gradient-to-br focus:ring-4 focus:ring-blue-300 dark:focus:ring-blue-800 shadow-lg shadow-blue-500/50 dark:shadow-lg dark:shadow-blue-800/80 font-medium rounded-lg text-sm px-5 py-2.5 text-center mr-2 mb-2"
          @click="creating = true"
        >
          Create
        </button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      creating: false,
    };
  },
};
</script>

<style scoped>
.app-container {
  min-height: calc(100vh - 60px);
}
</style>
