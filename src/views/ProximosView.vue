<template>
  <MainLayout>
    <template #next>
      <div class="container mx-auto back">
        <h1 class="mt-2 mb-5 fs-1">tvlike</h1>
        <img src="../../public/no-disponible.jpg" class="d-block w-100" alt="No disponible" />
      </div>
    </template>
  </MainLayout>
</template>
<script>
import MainLayout from '@/layouts/MainLayout.vue'
export default {
  components: { MainLayout }
}
</script>
<style>
.back {
  background: #1b2557d9;
  border-radius: 10px;
  padding: 7rem 0;
  margin-top: 8rem;
}

h1 {
  text-align: center;
  text-transform: uppercase;
  font-weight: bold;
  letter-spacing: 5px;
  color: rgb(209, 13, 13);
}
</style>
