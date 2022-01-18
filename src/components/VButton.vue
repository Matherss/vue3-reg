<template>
  <button @click="$parent.save()">Зарегистрироваться</button>
</template>

<script>
export default {};
</script>

<style scoped>
button {
  width: 300px;
  height: 50px;

  background: #745eff;
  color: white;
  border: 1px solid rgba(0, 0, 0, 0.2);
  box-sizing: border-box;
  cursor: pointer;
  transition: all 0.3s;
}
button:hover {
  background: white;
  color: #745eff;
  border: 1px solid #745eff;
}
button:active {
  border: 1px solid rgba(0, 0, 0, 0.2);

  box-shadow: 0px 0px 20px -4px #745eff;
}
@media screen and (max-width: 320px) {
  button {
    width: 260px;
  }
}
</style>
>
