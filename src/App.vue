<template>
  <!-- <section class="container">
    <h2>{{ user.name }}</h2>
    <h3>{{ user.age }}</h3>
  </section> -->
  <section class="container">
    <h2>{{ user2.name }}</h2>
    <h3>{{ user2.age }}</h3>
    <button @click="setAge">Change Age</button>
  </section>
</template>

<script>
import { reactive } from 'vue';
export default {
  setup(){
    // const user = ref({
    //   name: 'Maximilian',
    //   age: 31
    // }),
    //reactive() only works with objects
    const otherUser = reactive({
      name: "Samantha",
      age: 34
    })
    function setNewAge(){
      //dont forget to append .value when changing values of refs
      otherUser.age = 32
    }
    // const uName = ref('Maximilian');
    // const uAge = ref(31)
    // setTimeout(()=>{
    //   // uName.value = 'Max',
    //   // uAge.value = 35
    //   // user.value.name = 'Max',
    //   // user.value.age = 35,
    //   otherUser.name = "Sam",
    //   otherUser.age = 37
    // },2000)
    //to use ref() correctly with an object, pass the object to return and then access object properties
    //inside the template for it to be reactive
    return { user2: otherUser, setAge: setNewAge}
  }
  // data() {
  //   return {
  //     userName: 'Maximilian',
  //   };
  // },
};
</script>

<style>
* {
  box-sizing: border-box;
}

html {
  font-family: sans-serif;
}

body {
  margin: 0;
}

.container {
  margin: 3rem auto;
  max-width: 30rem;
  border-radius: 12px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.26);
  padding: 1rem;
  text-align: center;
}
</style>