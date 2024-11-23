<template>
    <div id="app" class="form-container">
        <h2>User Registeration </h2>

        <form @handleSubmit.prevent="handleSubmit">
                <!-- name  -->
                <div>
                    <label for="name">Name</label>
                    <input type="text" id="name" v-model="form.name">
                </div>
                <!-- email -->
                <div>
                    <label for="email">Email</label>
                    <input type="email" id="email" v-model="form.email">
                </div>
                
      <!-- Password Input -->
      <div>
        <label for="password">Password:</label>
        <input type="password" id="password" v-model="form.password" />
      </div>
      <!-- Password Input -->
      <div>
        <label for="password">Password:</label>
        <input type="password" id="password" v-model="form.password" />
      </div>

        </form>
    </div>
</template>




<script setup>
import { reactive } from "vue";

const form = reactive({
  name: "",
  email: "",
  password: "",
  age: null,
  terms: false,
  gender: "",
  country: "",
  bio: "",
});

const handleSubmit = () => {
  alert("Form Submitted!");
  console.log(form);
};
</script>

<style>
.form-container {
  max-width: 500px;
  margin: 0 auto;
}
div {
  margin-bottom: 15px;
}
label {
  display: block;
  margin-bottom: 5px;
}
input,
select,
textarea,
button {
  width: 100%;
  padding: 8px;
  margin: 5px 0;
}
textarea {
  height: 100px;
}
.preview {
  margin-top: 20px;
}
</style>
