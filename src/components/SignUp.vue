<template>
<img src="../assets/r1.png" alt="">
<h1>Sign Up</h1>
<div class="register">
    <input type="text" v-model="name" class="register-input" name=""  placeholder="Enter Name" id="">
    <input type="text"  v-model="email"  class="register-input" name="" id="" placeholder="Enter Email">
    <input type="password"  v-model="password"  class="register-input" name="" id="" placeholder="Enter Password">
    <button class="btn-signup" v-on:click="signUp">Sign Up</button>
</div>
<p>
    <router-link to="/login" class="btn-signup">Login</router-link>
</p>
</template>


<script>
import axios from 'axios';
export default {
    name: "SignUp",
    data(){
        return {
            name:"",
            email:"",
            password:""
        }
    },
    methods:{
        async signUp(){

            // console.warn("signup: ",this.email,this.name,this.password);
            let result = await axios.post("http://localhost:3000/users",{
                email: this.email,
                password:this.password,
                name:this.name,
            });
            console.log(result);
            if(result.status == 201){
                // alert("signup");
                localStorage.setItem("User-info",JSON.stringify(result.data));
                this.$router.push({name:"Home"});
            }
        }
    },
    mounted(){
        let user = localStorage.getItem("User-info");
        if(user){
            this.$router.push({name:"Home"});
        }
    }

}
</script>
<style>
    .register-input{
        width: 300px;
        height: 40px;
        display: block;
        padding-left: 20px;
        margin-bottom: 30px;
        margin-right: auto;
        margin-left: auto;
    }
    .btn-signup{
        width: 100px;
        outline: none;
        padding: 10px;
        text-align: center;
        border: none;
        border-radius: 10px;
        color: white;
        background: red;
    }
    .btn-signup:hover{
        cursor: pointer;
        background: black;
    }
</style>