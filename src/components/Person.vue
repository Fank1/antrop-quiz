<template>
  <div class="person">
    <img class="photo" :src="data.imgSrc" />
    <h2>Vem är detta?</h2>
    <p class="answer">
      <span>{{ data.firstName }}</span>
      <span>{{ data.lastName }}</span>
    </p>
  </div>
</template>

<script>
export default {
  name: "Person",
  props: {
    data: Object,
  },
};
</script>


<style scoped>
.photo {
  width: 100%;
  max-width: 200px;
  border-radius: 100%;
}
.answer {
  display: none;
}
</style>