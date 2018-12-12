<template>
    <div class="pre">
        <b-card>
        <h1>Question {{question.qid}}</h1>
            <div class="row">
                <input class="input" type="text" v-model="question.qname" placeholder="Input your question ..." />  
                       
                </div>
                <input type="text" class="input2" v-model="newchoice" placeholder="Add Choice ...">
                <b-button class="buttonCSS3" v-on:click="add()">Add</b-button>

                <!-- <b-radio name="choice" v-for="ch in this.question.ans" :key="ch.option" class="input5" id="radio" ><h2>
                    {{ch.option}}</h2></b-radio> -->
                    <div class="tt">
                <h4>
                    <input type="text" class="input8" v-for="ch in this.question.ans" :key="ch.option" v-model="ch.option">
                </h4> 
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
            surveys: [],
            newchoices :[], // radio
            newchoice:'' //text   
          
        }
    },
    
    firestore (){
        return {
            surveys : firestore.collection('surveys')
        }
    },

    methods:{
        save(key){
           
            var id = 'q'+this.question.qid;
            console.log('update--'+id);
        
            this.$firestore.surveys.doc(key).update({qid:this.question.qid,qname:this.question.qname,type:"qradio",
            ans:this.question.ans})
        },
         add() {
            
            console.log(this.newchoice);
            this.question.ans.push({
                option:this.newchoice
                });
            console.log(this.newchoices);
 
        },
        cancel(key){
            this.$firestore.surveys.doc(key).delete()
        }
    }
}

</script>

<style scoped>
.tt{
    margin-left: 17vh;
}
.input8 {
  width: 35vw;
  height: 6vh;
  margin-top: 2vh;
  font-size: 2.5vh;
   margin-right: 2vw;
}
.input5 {
  width: 70vw;
  height: 11vh;
  font-size: 18px;
  margin-top: 2vh;

}
p{
    color: black;
}
.input{
    width: 90vw;
    height: 11vh;
    font-size: 20px;
    margin-left: 3vh;
}
.input2{
    font-size: 20px;
    width: 40vw;
    height: 8vh;
    margin-top: 2vh;
    margin-left: 45vh;
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
.buttonCSS4{
  background-color: 	#1E90FF;
  width: 10vw;
  height: 8vh;
  font-size: 3.5vh;
}
.buttonCSS3{
  background-color:Orange;
  width: 7vw;
  height: 7vh;
  font-size: 3vh;
  margin-left: 50px;
}
h1 {
  color: rgb(0, 0, 0);
}
h2 {
  color: rgb(24, 22, 22); 
}
.img-body {
  height: 20vh;
}
.pre{
margin-top: 4vh;
margin-left: 2vw;
margin-right: 2vw;
margin-block-end: 2vh;
}
.card-body{
  width: 95vw;
  height:auto;
  text-align: left;
}
.col{
  text-align: center;
}
.row{
  margin-top: 2vh;
}
</style>
