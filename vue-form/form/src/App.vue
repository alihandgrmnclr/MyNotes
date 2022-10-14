<script setup>
import { ref, computed } from 'vue';
import InputText from './components/InputText.vue';
import InputEmail from './components/InputEmail.vue';

const formInputs = ref({
  name: "",
  lastname: "",
  email: "",
  reEmail: ""
});

const isFormValid = computed(() => {
  return Object.values(formInputs.value).every(input => input != "");
});

const submitHandler = async event => {
  event.preventDefault();
  
  console.log(isFormValid.value);
  if (!isFormValid.value) return;
  console.log("sended");

  const result = await fetch("https://jsonplaceholder.typicode.com/posts", {
    method: "POST",
    body: JSON.stringify({
      name: formInputs.value.name,
      lastname: formInputs.value.lastname,
    })
  }).then(data => data.json());

  return result;
};

</script>

<template>
  <form class="form" @submit="submitHandler" action="">
  FormInputs: {{formInputs}} <br><br>

    <InputText v-model:name="formInputs.name" label="Name"></InputText>
    <InputText v-model:name="formInputs.lastname" label="Surname"></InputText>

    <InputEmail v-model:email="formInputs.email" label="Mail"></InputEmail>
    <InputEmail v-model:email="formInputs.reEmail" label="Re-Email"></InputEmail>

    <button type="submit" class="form__button">Send</button>

  </form>
</template>

<style scoped>
.form{
  width: 300px;
}
</style>
