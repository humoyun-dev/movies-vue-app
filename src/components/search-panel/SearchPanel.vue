<template>
  <input
    type="text"
    class="form-control search-input"
    placeholder="Kinolarni qidirish"
    :value="text"
    @input="onChange"
  />
</template>

<script>
export default {
  data() {
    return {
      text: "",
    };
  },
  methods: {
    onChange(e) {
      this.text = e.target.value;
      this.$emit(`onUpdateTerm`, this.text);
    },
  },
};
</script>

<style scoped>
.search-input {
  margin-bottom: 1.5rem;
  padding: 1.5rem;
  background-color: #fcfaf5;
  border-radius: 4px;
  box-shadow: 15px 15px 15px rgba(0, 0, 0, 0.15);
}
</style>
