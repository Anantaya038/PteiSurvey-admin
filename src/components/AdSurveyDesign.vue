<template>
    <div>
        <!-- <div>
        <router-link to="/adminhome">
                <b-button class="btn">  <b-img :src="require('../photo/b.png')" class="img-body2"></b-img></b-button>
        </router-link>
        <h1>New Question</h1>
        <div>
            <router-link to="/newquestion">
                <b-button class="btn">  <b-img :src="require('../photo/add.png')" class="img-body"></b-img></b-button>
            </router-link>     
                   
            <b-button v-for="ch in surveys" v-bind:key="ch.qid" v-on:click="send(ch.qid)">
                Question {{ch.qid}} 
            </b-button> 
        </div>
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
      <tr>
          <th><h5>New Question</h5></th>
          <th><router-link to="/newquestion">
                <b-button class="btn">  <b-img :src="require('../photo/add.png')" class="img-body"></b-img></b-button>
            </router-link>     </th>
      </tr>
    <tr  v-for="ch in surveys" v-bind:key="ch.qid" v-on:click="send(ch.qid)">
          <th><h5>Question {{ch.qid}}</h5></th> 
          <th> <b-button><h5>Question {{ch.qid}}</h5></b-button></th>
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
        }
    },
    firestore (){
        return {
            surveys : firestore.collection('surveys').orderBy('qid')
        }
    },
    methods:{
        send(id){
            this.$router.push({ path:'./surveydetail/'+id })
            //วิทีส่งค่า
        }
    }
}
</script>

<style scoped>
.btn{
    width: 12vw;
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
.img-body{
    height: 5.5vh; 
}
</style>
