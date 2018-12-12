<template>
    <div style="margin: auto; margin-top:14vh; margin-left:30vw;margin-right:30vw;">
                <div class="img">
                    <b-img :src="require('../photo/page1.png')" class="img-body"></b-img>
                </div><br><br><br>
                <!-- <h1>PTEI Survey Designer</h1> -->

                <b-form-input class="input" type="email" v-model="email" placeholder="Enter E-mail"></b-form-input>
                <b-form-input class="input" type="password" v-model="password" placeholder="Enter Password"></b-form-input>
                <b-button class="btn" v-on:click="login()">Login</b-button>
    </div>
</template>

<script>
import firebase from 'firebase';

export default {

     data (){
        return{
            email:'',
            password:''
            
        }
    },
    methods:{
        login(){

             firebase.auth().signInWithEmailAndPassword(this.email, this.password)
                .then(() => {
                    alert('Log In Complete : '+this.email );
                    this.$router.push('/adminhome');
                })
                .catch((err) => {
                    alert(err.message);
                });
            
        }
    }
    
}
</script>


<style scoped>
    .card-body{
        text-align: center;
        border-radius: 20%;
    }
    .img{
        height: 35vh;  
        text-align: center;
    }
     .btn{
        margin-top: 2vh;
        color: black;
        width: 40vw;
        height: 7vh;
        border:1px solid #193C6C;
    }
    .input{
        width: 40vw;
        height: 7vh;
        margin: auto;
        margin-top: 1vh;
        font-size: 3vh;
    }
    .input::placeholder{
        font-weight: bold;
    }
    h1{
        text-align: center;
        color: white;
    }
</style>
