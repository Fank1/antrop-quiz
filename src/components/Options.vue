<template>
  <div class="options">
    <Option
      @submitted="handleSubmission"
      v-for="(option, index) in this.optionData"
      class="option"
      :key="index"
      :data="option"
      :currentPerson="this.currentPerson"
      :orderNumber="orderRandomizer()"
    />
  </div>
</template>

<script>
import Option from "./Option.vue";
export default {
  name: "Options",
  data() {
    return {
      options: null,
    };
  },
  methods: {
    handleSubmission() {
      this.$emit("submitted-to-parent");
    },
    orderRandomizer() {
      let random = Math.floor(Math.random() * this.numOfOptions);
      return random;
    },
  },
  components: {
    Option,
  },
  props: {
    currentPerson: Object,
    optionData: Array,
    numOfOptions: Number,
  },
};
</script>


<style scoped>
</style>