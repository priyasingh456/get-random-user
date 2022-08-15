<template>
  <div id="app">
    <img :src="picture" :alt="firstName" :class="gender"/>
    <h1>{{title}} {{firstName}} {{lastName}}</h1>
    <p>Email: {{email}}</p>
    <button @click="getUser" type="submit" :class="gender">Get Random User</button>
  </div>
</template>



<script>

export default {
  name: 'App',

  data(){
    return {
      title: 'Mr.',
      firstName: 'John',
      lastName: 'Doe',
      email: 'john.doe@exapmle.com',
      gender: 'male',
      picture: "https://randomuser.me/api/portraits/men/53.jpg"
    }
  },

  methods: {
    async getUser(){
      const res = await fetch('https://randomuser.me/api');
      const { results } = await res.json();
      //console.log(results);

      this.title = results[0].name.title,
      this.firstName = results[0].name.first,
      this.lastName = results[0].name.last,
      this.email = results[0].email,
      this.gender = results[0].gender,
      this.picture = results[0].picture.large
    }
  }
}
</script>



<style scoped>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 100px;
}

img{
  width: 13%;
  border-radius: 50%;
}

.male{
  border: 8px rgb(137, 224, 253) solid;
  background-color: rgb(137, 224, 253);
}

.female{
  border: 8px rgb(251, 148, 234) solid;
  background-color:rgb(251, 141, 233);
}

button{
  padding: .5rem 3rem;
  border-radius: 5px;
  cursor: pointer;
}
</style>
