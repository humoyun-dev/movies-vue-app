<template>
  <div class="app-info">
    <p class="fs-3 text-uppercase">Barcha kinolar soni: {{ moviesCount }}</p>
    <p class="fs-4 text-uppercase">
      Ko'rilgan kinolar soni: {{ favouriteCount }}
    </p>
  </div>
</template>

<script>
export default {
  props: {
    moviesCount: {
      type: Number,
      required: true,
    },
    favouriteCount: {
      type: Number,
      required: true,
    },
  },
};
</script>

<style scoped>
.app-info {
  padding: 1.5rem;
  border-radius: 4px;
  box-shadow: 15px 15px 15px rgba(0, 0, 0, 0.15);
  background-color: #fcfaf5;
}
</style>
