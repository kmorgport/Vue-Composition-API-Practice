<template>
  <!-- <section class="container">
    <h2>{{ user.name }}</h2>
    <h3>{{ user.age }}</h3>
  </section> -->
  <section class="container">
    <user-data 
    :first-name="firstName"
    :last-name="lastName"
    :age="age"></user-data>
    <h2>{{ user2.name }}</h2>
    <h3>{{ user2.age }}</h3>
    <button @click="setAge">Change Age</button>
    <div>
      <!-- v-model accepts refs and reactives -->
      <input type="text" placeholder="First Name" v-model="firstName"/>
      <input type="text" placeholder="Last Name" ref="lastNameInput"/>
      <button @click="setLastName">Set Last Name</button>
    </div>
  </section>
  <section>
    <h2>{{ uName}}</h2>
  </section>
</template>

<script>
import UserData from './components/UserData.vue'
import { ref, reactive, computed, watch } from 'vue';
export default {
  components:{
    UserData
  },
  setup(){
    // const user = ref({
    //   name: 'Maximilian',
    //   age: 31
    // }),
    //reactive() only works with objects
    const firstName = ref('')
    const lastName = ref('')
    const lastNameInput = ref(null);
    const otherUser = reactive({
      name: "Samantha",
      age: 34
    })
    function setNewAge(){
      //dont forget to append .value when changing values of refs
      otherUser.age = 32
    }

    // watch(firstName, function(newValue, oldValue) {
    //   console.log('Old name '+oldValue);
    //   console.log("new name " + newValue)
    // })

    //when you have more than one dependency 

    watch([firstName, lastName], function(newValues, oldValues){
        console.log('Old first name '+oldValues[0]);
        console.log("new first name " + newValues[0])
        console.log('Old last name '+oldValues[1]);
        console.log("new last name " + newValues[1])
    })





    // function setFirstName(event){
    //   firstName.value = event.target.value;
    // }
    // function setLastName(event){
    //   lastName.value = event.target.value;
    // }
    //computed refs are read only. not read and write 
    const uName = computed(()=>{
      return firstName.value + ' ' + lastName.value
    })
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


    //<-- using refs with Composition API -- >//
    function setLastName(){
      //can't use this.$refs
      //must use value.value 
      //one value for the ref()
      //other value for the input element ref
      lastName.value = lastNameInput.value.value;
    }
    return { 
      user2: otherUser,
       setAge: setNewAge,
      firstName,
      lastNameInput,
      setLastName,
      uName,
      lastName
       }
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