<script setup>
import { ref,computed } from 'vue';

const firstname = ref("Donoxon");
const lastname = ref("Masalan");
const email = ref("masalandonoxon@gmail.com");
const phoneNumber = ref("97-248-978-464")
const imgage = ref("https://www.shutterstock.com/image-photo/happy-attractive-young-adult-woman-260nw-2458168305.jpg")
const gender = ref("female");

const fullName = computed(() => `${firstname.value} ${lastname.value}`);

const checkGender = computed(() =>({
  "border-blue-500": gender.value === "male",
  "border-pink-500": gender.value === "female",
}));

const randomUser = async () => {
  try{
    const res = await fetch("https://randomuser.me/api/");
   if (!res.ok) {
    throw new Error( `Server error: ${res.status}` );
   }
    const { results } = await res.json();
    console.log(res);

    const user = results[0];
    console.log(user);

firstname.value = user.name.first;
lastname.value = user.name.last;
email.value = user.email;
gender.value = user.gender;
phoneNumber.value = user.phone;
imgage.value = user.picture.large;

  }catch (error) {
console.log("error" , error);
  }
}

</script>
<template>
  <div class="flex justify-center items-center min-h-screen">
    <div class="flex flex-col justify-center items-center">
      <div class="relative mb-8">
        <div class="absolute left-1/2 -top-2 bg-white rounded-full px-4 text-lg transform -translate-x-1/2">{{ gender }}</div>
        <img 
        class="w-64 h-64 rounded-full border-8" 
        :class="checkGender"
        :src="imgage" :alt="firstname" />
      </div>
      <div class="text-center space-y-1">
        <h1 class="text-4xl font-bold"> Hi, My name is {{ fullName }}</h1>
        <p class="text-lg text-gray-500">{{ email }}</p>
        <p class="text-lg text-gray-500">{{ phoneNumber }}</p>
      </div>
      <button @click="randomUser" class="bg-black text-white px-6 py-2 rounded font-bold mt-6">Random user</button>
    </div>
  </div>
</template>