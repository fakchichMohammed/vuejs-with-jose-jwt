<script setup>
import { ref, onMounted, onUpdated } from "vue";
import * as jose from "jose";

const token = ref("");
const decodedToken = ref("");
const tokenFromLocalStorage = ref("");

function decodeToken() {
  try {
    decodedToken.value = jose.decodeJwt(token.value);
    console.log(decodedToken.value);
    window.localStorage.setItem("token", token.value);
    
  } catch (error) {
    decodedToken.value = error.message
  }
}

function getToken() {
  const token = window.localStorage.getItem("token");
  if (token !== null) {
    tokenFromLocalStorage.value = token;
  } else {
    tokenFromLocalStorage.value = "No token found!";
  }
}

getToken() 

</script>
<template>
  <hr />
  <h1>Ex : 1 - 2 - 3</h1>
  <input type="text" v-model="token" />
  <button @click="decodeToken">decode</button>
  <p>{{ decodedToken }}</p>
  <hr />
  <h1>Ex : 4</h1>
  <p>{{ tokenFromLocalStorage }}</p>
</template>
<style>
</style>
