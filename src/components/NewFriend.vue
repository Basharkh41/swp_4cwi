<template>
  <form @submit.prevent="addFriend">
    <h2>Add a new contact</h2>
    <label for="fname">First name:</label><br />
    <input v-model="fname" type="text" id="fname" name="fname" /><br />

    <label for="lname">Last name:</label><br />
    <input v-model="lname" type="text" id="lname" name="lname" /><br />
    
    <label for="age">Age:</label><br />
    <input v-model="age" type="number" id="age" name="age" /><br />
    
    <label for="number">Number:</label><br />
    <input v-model="number" type="number" id="number" name="number" /><br />

    <label for="email">Email: </label><br />
    <input v-model="email" type="email" id="email" name="email" /><br />
    <button>Add</button>
  </form>
</template>
<script>
export default {
  emits: ["add-contact"],
  data() {
    return {
      fname: " ",
      lname: " ",
      age: " ",
      number: " ",
      email: " ",
    }; 
  },
  methods: {
    addFriend() {
      console.log(this.fname, this.lname, this.age, this.number, this.email);
      this.$emit("add-contact",this.fname, this.lname, this.age, this.number, this.email);

    },
  },
};
</script>