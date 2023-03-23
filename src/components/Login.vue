<template>
    <img src="../assets/r1.png" alt="">
    <h1>Sign Up</h1>
    <div class="register">
        <input type="text"  v-model="email"  class="register-input" name="" id="" placeholder="Enter Email">
        <input type="password"  v-model="password"  class="register-input" name="" id="" placeholder="Enter Password">
        <button class="btn-signup" v-on:click="login">Login</button>
    </div>
    <p>
        <router-link to="/sign-up" class="btn-signup">SignUp</router-link>
    </p>
    </template>
    
<script>
import axios from 'axios';
    export default{
        name:"LoginComponent",
        data(){
            return {
                email:"",
                password:""
            }
        },
        methods:{
            async login(){
                console.log(this.email,this.password);
                let result = await axios.get(`http://localhost:3000/login?email=${this.email}&password=${this.password}`)
                if(result.status==200){
                    localStorage.setItem("user-info",JSON.stringify(result.data))
                    this.$router.push({name:"Home"});
                }
                console.log(result);

            }
        },
    }
</script>