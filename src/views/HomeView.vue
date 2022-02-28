<script setup>
import SimpleCard from "@/components/SimpleCard.vue";
</script>

<template>
  <div class="dark:bg-gray-900 app-container">
    <div class="container items-center mx-auto p-5">
      <div class="grid grid-cols-4 gap-4">
        <SimpleCard to="/medicines" title="MEDICINES" description="Here you can manage your medicines" />
        <SimpleCard to="/promotions" title="PROMOTIONS" description="Here you can manage the promotions" />
        <SimpleCard to="/invoices" title="INVOICES" description="Here you can manage the invoices" />
      </div>
    </div>
  </div>
</template>

<style scoped>
.app-container {
  min-height: calc(100vh - 60px);
}
</style>
