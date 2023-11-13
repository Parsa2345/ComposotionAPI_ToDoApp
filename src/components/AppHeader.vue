<template>
  <header class="card">
    <h1>لیست وظایف </h1>

    <button @click="changeTheme" id="theme-switcher">
      <img v-if="defaultTheme=='dark'" :src="Sun" alt="Change color theme" />
      <img v-else :src="Moon" alt="Change color theme" />
    </button>
  </header>
</template>

<script setup>
import Sun from "../assets/images/icon-sun.svg";
import Moon from "../assets/images/icon-moon.svg";
import {ref} from "vue";
 
     const defaultTheme=ref("dark");
 
  
   function changeTheme(){
      if (defaultTheme.value=="dark") {
        defaultTheme.value="light";
        document.querySelector("body").classList.add("light");
      } else {
        defaultTheme.value="dark";
        document.querySelector("body").classList.remove("light");

      }
    }
 

</script>
<!-- <script> 
import Sun from "../assets/images/icon-sun.svg";
import Moon from "../assets/images/icon-moon.svg";
export default 
{
  name:"AppHeader",
  data() {
    return {
      sunImage:Sun,
      moonImage:Moon,
      defaultTheme:"dark",
    };
  },
  methods: {
    changeTheme(){
      if (this.defaultTheme=="dark") {
        this.defaultTheme="light";
        document.querySelector("body").classList.add("light");
      } else {
        this.defaultTheme="dark";
        document.querySelector("body").classList.remove("light");

      }
    }
  },

};

</script> -->