<template>
  <input
    :type="data.type"
    :placeholder="data.placeholder"
    :value="modelValue"
    @input="updateInput"
  />
</template>

<script>
export default {
  name: "my-input",
  props: {
    data: {
      type: Object,
      required: true,
    },
    modelValue: [String, Number],
  },
  methods: {
    updateInput(event) {
      this.$emit("update:modelValue", event.target.value);
    },
  },
};
</script>

<style scoped>
input {
  width: 100%;
  height: 30px;
  padding: 2px 5px;
}
</style>