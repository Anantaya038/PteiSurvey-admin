<template>
    <div>
        
        <!-- <router-link to="/view">
                <b-button class="button1">  <b-img :src="require('../photo/b.png')" class="img-body2"></b-img></b-button>
        </router-link>
        <h1>Point of View of Tourist</h1>

        <div>    
            
            <b-button class="buttonCSS" v-for="(ch,index) in answers" v-bind:key="ch.id" v-on:click="send(index)">
                Tourist {{++index}} 
            </b-button>
        </div>
         -->
         <div class="pre">
       <table class="table table-dark table-striped">
  <thead class="center">
    <tr>
      <th><h3>Tourist No.</h3></th>
      <th><h3>Point of View of Tourist</h3> </th>
    </tr>
  </thead> 
  <tbody>
    <tr v-for="(ch,index) in answers" v-bind:key="ch.id" v-on:click="send(index)">
          <th><h5> {{++index}}</h5></th> 
          <th><b-button><h5>Tourist {{index}}</h5></b-button></th>
       </tr>
       </tbody>
       </table>
    </div>
    </div>
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
            surveys : firestore.collection('surveys')
        }
    },
    methods:{
        send(id){
            console.log(id);
           // this.tourist = id;
            this.$router.push({ path:'./adviewdetail/'+id })
            
            //วิทีส่งค่า
        }
    }
}
</script>

<style scoped>
.center,th{
    text-align: center;
}
.pre{
margin-top: 2vh;
margin-left: 2vw;
margin-right: 2vw;
margin-block-end: 2vh;
}
.btn{
    width: 18vw;
}
</style>
