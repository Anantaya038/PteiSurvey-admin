<template>
    <div style="margin-top: 1vh">
        <!-- <router-link to="/view">
                <b-button class="button1">  <b-img :src="require('../photo/b.png')" class="img-body2"></b-img></b-button>
        </router-link>
        <h2>Point of View of Question</h2>
         -->
        <!-- <div>
            <router-link to="/allquestion">
                <b-button class="buttonCSS" >All Question </b-button>
            </router-link> 

            <b-button class="buttonCSS" v-for="(ch,index) in surveys" v-bind:key="ch.qid" v-on:click="send2(ch.qid)">
                Question {{++index}} 
            </b-button>
        </div> -->
<div class="pre">
       <table class="table table-dark table-striped">
  <thead class="center">
    <tr>
      <th><h3>Question No.</h3></th>
      <th><h3>Point of View of Question</h3> </th>
    </tr>
  </thead> 
  <tbody>
    <tr  v-for="(ch,index) in surveys" v-bind:key="ch.qid" v-on:click="send2(ch.qid)">
          <th><h5>Question {{++index}}</h5></th> 
          <th> <b-button><h5>Question {{index}}</h5></b-button></th>
       </tr>
       </tbody>
       </table>
    </div></div>
</template>

<script>
import {firestore} from '../firebase.js'

export default {

     data (){
        return{
            surveys:[],
            answers:[]
           // tourist:null
        }
    },
    firestore (){
        return {
            answers : firestore.collection('answers'),
            surveys : firestore.collection('surveys').orderBy("qid")
        }
    },
    methods:{
        
        send2(id){
            console.log(id);
            this.$router.push({ path:'./viewquestion/'+id })
        }
    }
}
</script>

<style scoped>
h2{
    color: rgb(0, 0, 0);
}
.img-body{

    height: 20vh; 
}
.img-body2{
    width: 7vh;
    height: 7vh; 
}
.btn{
    width: 18vw;
}
.center,th{
    text-align: center;
}
.pre{
margin-top: 2vh;
margin-left: 2vw;
margin-right: 2vw;
margin-block-end: 2vh;
}
</style>
