<template>
    <div class="pre">
        <b-card>
        <h1>Question {{question.qid}}</h1>
        <div class="row">
            <b-form-input class="input" type="text" v-model="question.qname" placeholder="Input your question ..." ></b-form-input>
            </div> <br>
        
            <!-- <b-button class="button1">  <b-img :src="require('../photo/y2.png')" class="col"></b-img></b-button>
           <b-button class="button1">  <b-img :src="require('../photo/no2.png')" class="col"></b-img></b-button> -->
        <div class="row">
           <div class="col"><b-img  :src="require('../photo/y2.png')" class="img-body"></b-img></div>
            <div class="col"><b-img :src="require('../photo/no2.png')" class="img-body"></b-img></div>
        </div>
        
       </b-card>
       <div class="row">
            <router-link to='/adsurveydesign' class="col">    
                    <b-button class="buttonCSS" v-on:click="save(question['.key'])"> Save</b-button>
                </router-link>

                <router-link to='/adsurveydesign'>
                    <b-button class="buttonCSS2" v-on:click="cancel(question['.key'])">Delete</b-button>
                </router-link>
                <!-- <b-button class="buttonCSS2" v-on:click="cancel()">Cancel</b-button>-->
                <router-link to='/adsurveydesign' class="col">
                    <b-button class="buttonCSS4" >Cancel</b-button> 
                </router-link>
                </div>   
    </div>
</template>


<script>
import {firestore} from '../firebase.js'

export default {
props:['question'],
    data (){
        return{
            newText: '',
            id:'',
            surveys: []
        }
    },
    
    firestore (){
        return {
            surveys : firestore.collection('surveys')
        }
    },
    methods:{
        save(key){
            console.log(this.newText);
            var length = this.surveys.length;
            var newQ = 'q'+length;
            var id = 'q'+this.question.qid;
            console.log(newQ);
            console.log('update--'+id);
            
            this.$firestore.surveys.doc(key).update({qid:this.question.qid,qname:this.question.qname,type:"q-yes-no"})
        },
        cancel(key){
           this.$firestore.surveys.doc(key).delete()
        }
    }
}
</script>


<style scoped>
.buttonCSS4{
  background-color: 	#1E90FF;
  width: 10vw;
  height: 8vh;
  font-size: 3.5vh;
}
p{
    color: black;
}
.input{
   width: 92vw;
  height:10vh;
    font-size: 20px;
    margin-left: 2.5vh;
}
.buttonCSS {
  width: 10vw;
  height: 8vh;
  font-size: 3.5vh;
}
.buttonCSS2{
  background-color: red;
  width: 10vw;
  height: 8vh;
  font-size: 3.5vh;
  text-align: center;
}
.button1 {
  background-color:inherit;
  border-radius:50%;
  width: auto;
  height: auto;
}
h1 {
  color: rgb(0, 0, 0);
}

.img-body {
  height: 25vh;
  width: 25vh;
}
.card-body{
  width:95vw;
  height:70vh;
  text-align: left;
}
.col{
  text-align: center;
  
}
.pre{
margin-top: 4vh;
margin-left: 2vw;
margin-right: 2vw;
margin-block-end: 2vh;
}

.row{
  margin-top: 2vh;
}
</style>
