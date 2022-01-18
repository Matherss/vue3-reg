<template>
  <div class="container">
    <div class="limiter">
      <h1>Регистрация</h1>
      <form action="#">
        <div class="input-errors" v-for="(error, index) of v$.email.$errors" :key="index">
          <div class="error-msg">{{ error.$message }}</div>
        </div>
        <v-input
          v-model="v$.email.$model"
          :model-value="email"
          @update:model-value="email = $event"
          placeholderText="Введите почту*"
        />
        <div class="input-errors" v-for="(error, index) of v$.password.$errors" :key="index">
          <div class="error-msg">{{ error.$message }}</div>
        </div>
        <v-input
          type="password"
          v-model="v$.password.$model"
          :model-value="password"
          @update:model-value="password = $event"
          placeholderText="Введите пароль*"
        />
        <div class="input-errors" v-for="(error, index) of v$.name.$errors" :key="index">
          <div class="error-msg">{{ error.$message }}</div>
        </div>
        <v-input
          v-model="v$.name.$model"
          :model-value="name"
          @update:model-value="name = $event"
          placeholderText="Введите имя*"
        />
        <v-button />
        <div v-if="successForm == true" style="color: green">Регистрация прошла успешно</div>
      </form>
    </div>
  </div>
</template>

<script>
import useVuelidate from "@vuelidate/core";
import { required, email, helpers } from "@vuelidate/validators";
import VButton from "./components/VButton.vue";
import VInput from "./components/VInput.vue";

export default {
  name: "App",
  setup() {
    return { v$: useVuelidate() };
  },
  validations() {
    return {
      email: {
        required: helpers.withMessage("Обязательное поле", required),
        email: helpers.withMessage("Невалидная почта", email)
      },
      password: {
        required: helpers.withMessage("Обязательное поле", required)
      },
      name: {
        required: helpers.withMessage("Обязательное поле", required)
      }
    };
  },
  components: {
    VInput,
    VButton
  },
  data() {
    return {
      successForm: false,
      email: "",
      password: "",
      name: "",
      arr: []
    };
  },
  methods: {
    save() {
      setTimeout(this.v$.$validate, 200);
      if (this.v$.$silentErrors.length > 0) {
        console.log("error");
      } else {
        this.successForm = true;
        console.log("work");
        this.arr.push({ email: this.email, password: this.password, name: this.name });

        const data = JSON.stringify(this.arr);
        window.localStorage.setItem("arr", data);
        console.log(JSON.parse(window.localStorage.getItem("arr")));
        document.querySelector("form").reset();
        setTimeout(() => {
          window.location.href = "https://hh.ru/vacancy/51060615";
        }, 1200);
      }
    }
  }
};
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Ubuntu:wght@300;400;500&display=swap");
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: "Ubuntu", sans-serif;
}
.container {
  background: url("assets/img/1.jpg");
  width: 100vw;
  height: 100vh;
  margin: 0 auto;
  display: flex;
  flex-direction: column;
  align-items: center;
}
.error-msg {
  color: red;
}

.limiter {
  max-width: 420px;
  height: 493px;
  text-align: center;
  background: rgba(255, 255, 255, 0.15);
  border-radius: 15px;
  margin-top: 15px;
  padding: 0px 15px 0px 15px;
  box-shadow: 0px 0px 27px -4px rgba(0, 0, 0, 0.2);
}
h1 {
  margin: 19px 25px 30px 25px;
  font-style: normal;
  font-weight: normal;
  font-size: 36px;
  line-height: 41px;
  text-align: center;

  color: #745eff;

  text-shadow: 0px 4px 4px rgba(0, 0, 0, 0.15);
}
@media screen and (max-width: 320px) {
  .container {
    width: 320px;
  }
  .limiter {
    width: 300px;
  }
}
</style>
