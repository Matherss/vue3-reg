<template>
  <input
    type="text"
    :value="modelValue"
    @input="$emit('update:modelValue', $event.target.value)"
    :placeholder="placeholderText"
  />
</template>

<script>
export default {
  name: "Input",

  props: ["modelValue", "placeholderText"],
  emits: ["update:modelValue"]
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
input {
  width: 300px;
  height: 50px;

  background: #ffffff;
  border: 1px solid rgba(0, 0, 0, 0.2);
  box-sizing: border-box;
  border-radius: 10px;
  outline: none;
  margin-bottom: 10px;
  padding: 5px;
}
input::placeholder {
  font-size: 20px;
  line-height: 28px;
  color: rgba(0, 0, 0, 0.3);
}
@media screen and (max-width: 320px) {
  input {
    width: 260px;
  }
}
</style>
