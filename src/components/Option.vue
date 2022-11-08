<template>
  <button v-on:click="onGuess" :style="{ order: this.orderNumber }">
    {{ data.firstName + " " + data.lastName }}
  </button>
</template>

<script>
export default {
  name: "Option",
  props: {
    data: Object,
    currentPerson: Object,
    orderNumber: Number,
  },
  emits: ["submitted"],
  methods: {
    onGuess() {
      if (this.data.id === this.currentPerson.id) {
        console.log("rätt svar");
        this.$emit("submitted");
      } else {
        console.log("fel svar");
      }
    },
  },
};
</script>

<style scoped>
button {
  font-size: 1rem;
  background: none;
  border: 1px solid #ccc;
  padding: 0.75rem 1rem;
  margin: 0.5rem;
  cursor: pointer;
}
button:hover {
  background-color: #eeeeff;
}
</style>