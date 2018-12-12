<template>
    <div class="pre">   
      <b-card>
        <h1>Question {{question.qid}}</h1>
        <div class="row">
            <b-form-input class="input" type="text" v-model="question.qtitle" placeholder="Input your title ..." ></b-form-input>
           
        </div> 
        <div> 
            <input type="text" class="input25" v-model="question.titleE" placeholder="Input ...">

            <b-button class="button1">  <b-img :src="require('../photo/n1.png')" class="img-body"></b-img></b-button>
            <b-button class="button1">  <b-img :src="require('../photo/n2.png')" class="img-body"></b-img></b-button>
            <b-button class="button1">  <b-img :src="require('../photo/n3.png')" class="img-body"></b-img></b-button>
            <b-button class="button1">  <b-img :src="require('../photo/n4.png')" class="img-body"></b-img></b-button>   
            <b-button class="button1">  <b-img :src="require('../photo/n5.png')" class="img-body"></b-img></b-button><br><br>

        </div>  
        <div> 
             <input type="text" class="input25" v-model="question.titleS" placeholder="Input ...">

            <b-button class="button1">  <b-img :src="require('../photo/s1.png')" class="img-body"></b-img></b-button>
            <b-button class="button1">  <b-img :src="require('../photo/s2.png')" class="img-body"></b-img></b-button>
            <b-button class="button1">  <b-img :src="require('../photo/s3.png')" class="img-body"></b-img></b-button>
            <b-button class="button1">  <b-img :src="require('../photo/s4.png')" class="img-body"></b-img></b-button>       
            <b-button class="button1">  <b-img :src="require('../photo/s5.png')" class="img-body"></b-img></b-button>     
        </div><br>
        <div>

            <input type="text" class="input2" v-model="newchoice" placeholder="Add sub question ...">
            <b-button class="buttonCSS3" v-on:click="add()">Add</b-button><br><br><br>

        </div>
        <div class="ee">
            <h4>
                <input type="text" class="input8" v-for="ch in this.question.qsub" :key="ch.option" v-model="ch.option">
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

            <router-link to='/adsurveydesign' class="col">
                <b-button class="buttonCSS4" >Cancel</b-button> 
            </router-link>
        </div>
    </div>
</template>


<script>
import { firestore } from "../firebase.js";

export default {
  props: ["question"],
  data() {
    return {
      newText: "",
      id: "",
      newInput: "",
      newInput2: "",
      surveys: [],
      newchoices: [], // radio
      newchoice: "" //text
    };
  },

  firestore() {
    return {
      surveys: firestore.collection("surveys")
    };
  },
  methods: {
    save(key) {
      console.log(this.newText);
      var length = this.surveys.length;
      var newQ = "q" + length;
      var id = "q" + this.question.qid;
      console.log(newQ);
      console.log("update--" + id);

      this.$firestore.surveys.doc(key).update({
        qid: this.question.qid,
        qsub:this.question.qsub,
        type: "qexpect",
        qtitle: this.question.qtitle,
        // input:this.question.input,input2:this.question.input2})
        titleE: this.question.titleE,
        titleS: this.question.titleS
      });
    },

    add() {

      console.log(this.newchoice);
      // this.question.qsub.push(this.newchoice);
      this.question.qsub.push({
        option: this.newchoice
      });
      console.log(this.newchoices);
    },

    cancel(key) {
      this.$firestore.surveys.doc(key).delete();
    }
  }
};
</script>


<style scoped>
.buttonCSS4 {
  background-color: 	#1E90FF;
  width: 10vw;
  height: 8vh;
  font-size: 3.5vh;
}
.ee{
  margin-left: 20vh;
}
.button1 {
  background-color: inherit;
  border-radius: 10px;
  border-color: inherit;
  width: 11vh;
  height: 11vh;
  margin-top: 10px;
  margin-right: 200px;
  margin-bottom: 10px;
  margin-left: 200vh;
}
.img-body2 {
  width: 7vh;
  height: 7vh;
}
.buttonCSS3 {
  background-color:Orange;
  width: 7vw;
  height: 7vh;
  font-size: 3vh;
  margin-left: 50px;
}
.input8 {
  width: 35vw;
  height: 6vh;
  margin-right: 2vw;
  margin-top: 2vh;
  font-size: 2.5vh;
}
.input2 {
  width: 35vw;
  height: 8vh;
  margin-right: 2vw;
  font-size: 20px;
  margin-left: 45vh;
}
p {
  color: black;
}
.input {
  margin-left: 3vh;
  width: 90vw;
  height: 11vh;
  font-size: 20px;
}
.input25 {
  width: 35vw;
  height: 8vh;
  font-size: 20px;
  margin-left: 18vh;
}
.buttonCSS {
  width: 10vw;
  height: 8vh;
  font-size: 3.5vh;
}
.buttonCSS2 {
  background-color: red;
  width: 10vw;
  height: 8vh;
  font-size: 3.5vh;
  text-align: center;
}
.button1 {
  background-color:inherit;
  border-radius:inherit;
  width: auto;
  height: auto;
  border-radius: 50%;
  margin-top: 5px;
  margin-right: 5px;
  margin-bottom: 5px;
  margin-left: 5px;
}
h1 {
  color: rgb(0, 0, 0);
}
.img-body {
  height: 9vh;
  width: 9vh;
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
