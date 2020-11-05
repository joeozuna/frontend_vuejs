<template>
    <div class="home">
    <div class="wrapper fadeInDown">
      <div id="formContent">
        <!-- Tabs Titles -->

        <!-- Icon -->
        <div class="fadeIn first">
          <img
            src="@/assets/logo.png"
            id="icon"
            alt="User Icon"
          />
        </div>

        <!-- Login Form -->
        <form v-on:submit.prevent="register">
                <input type="text" id="name" class="fadeIn second" name="name" placeholder="Nombre" v-model="name">
                <input type="text" id="last_name" class="fadeIn second" name="last_name" placeholder="Apellidos" v-model="last_name">
                <input type="text" id="address" class="fadeIn second" name="address" placeholder="Direccion" v-model="address">
                <input type="text" id="phone_number" class="fadeIn second" name="phone_number" placeholder="Telefono" v-model="phone_number">
                <input type="text" id="email" class="fadeIn second" name="email" placeholder="Email" v-model="email">
                <input type="text" id="password" class="fadeIn third" name="password" placeholder="Password" v-model="password">
                <input type="submit" class="fadeIn fourth" value="Registrarme">
        </form>

        <!-- Remind Passowrd -->
          <div class="alert alert-danger" role="alert" v-if="error">
                  {{error_msg}}
          </div>
      </div>
    </div>
  </div>
</template>


<script>
import axios from 'axios';

export default {
    name: "Registro",
    components: {

    },
  data: function(){
    return{
      name: "",
      last_name: "",
      address: "",
      phone_number: "",
      email: "",
      password: "",
      error_msg: "",
    }
  },
  methods:{
    register(){
      let json = {
        "name": this.name,
        "last_name": this.last_name,
        "address": this.address,
        "phone_number" : this.phone_number,
        "email" : this.email,
        "password" : this.password,
      };
      axios.post('http://localhost:8000/api/register', json)
      .then( data =>{
           if(data.data.status == "ok"){
             //localStorage.token = data.data.token;
             this.$router.push('/');
           }else{
             this.error = true;
             this.error_msg = data.data.error_msg;
           }
      })
    }
  }
}
</script>

<style scoped>

</style>