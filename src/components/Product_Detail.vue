<template>
  <v-container>
    <h1 class="text-center">Detail</h1>
    <hr>
    <h2 class="fw-light fs-6">{{ productid }}. {{ description }}</h2>
  </v-container>
</template>

<script>
export default {
  data() {
    return {
      productid: this.$route.params.id,
      description: this.$route.params.description,
    };
  },
};
</script>

<style></style>
