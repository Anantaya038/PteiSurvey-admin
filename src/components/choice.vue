<template>
    <div class="pre">
          <b-card >
            <h2>Input your question</h2>
            <div>
                <input class="input" type="text" v-model="newText" placeholder="Input your question ..." /><br><br>  
                 <h2>Input your choice</h2>
                 <div class="row">
                <input type="text" class="input2" v-model="newchoice" placeholder="Add Choice ...">
                <b-button class="buttonCSS3" v-on:click="add()">Add</b-button>
               </div>
               <div class="ee">
                <b-radio name="choice" v-for="ch in this.newchoices" :key="ch" class="input5" id="radio" ><h2>{{ch}}</h2></b-radio>
        </div>
            </div>
                   
          </b-card>  
          <div class="row">
             <router-link class="col" to="/newquestion">
                <b-button class="buttonCSS" v-on:click="save()">Save</b-button>
            </router-link>
            <router-link class="col" to="/newquestion">
                <b-button class="btnred" >Cancel</b-button>    
            </router-link>
            </div>       
    </div>
</template>

<script>
import { firestore } from "../firebase.js";

export default {
  data() {
    return {
      newText: "",
      id: "",
      surveys: [],
      newchoices: [], // radio
      newchoice: "", //text
      newc: {}
    };
  },

  firestore() {
    return {
      surveys: firestore.collection("surveys")
    };
  },

  methods: {
    save() {
      console.log(this.newText);
      var length = this.surveys.length + 1;
      var newQ = "q" + length;
      var id = length++;
      console.log(newQ);
      console.log(id);

      var newdatas = []
      for (var i = 0; i < this.newchoices.length; i++) {
        var newdata = {
          option: this.newchoices[i]
        };
        newdatas.push(newdata);
      }
  

      this.$firestore.surveys.doc().set({qid: id, qname: this.newText, type: "mchoice",
      // ans: this.newchoices});
         ans: newdatas});
    },
    add() {
      console.log(this.newchoice);
      this.newchoices.push(this.newchoice);
      console.log(this.newchoices);
      
    }
    // cancel() {
    //   var length = this.surveys.length;
    //   var newQ = "q" + length;

    //   this.$firestore.surveys.doc(newQ).delete();
    // }
  }
};
</script>

<style scoped>
.card {
  width: auto;
  height: auto;
}
p {
  color: black;
}
.input {
  width: 92vw;
  height:10vh;
  font-size: 20px;
}
.input5 {
  width: 70vw;
  height: 11vh;
  font-size: 18px;
  margin-top: 2vh;
  margin-bottom: -15vh;
}
.ee{
  margin-left: 30vh;
}
.input2 {
  width: 40vw;
  height: 8vh;
  font-size: 20px;
  margin-left: 18vw;
}
.buttonCSS {
  width: 10vw;
  height: 8vh;
  font-size: 3.5vh;
  text-align: center;
}
.btnred {
  background-color: red;
  width: 10vw;
  height: 8vh;
  font-size: 3.5vh;
  text-align: center;
}
.buttonCSS3 {
  background-color: Orange;
  width: 10vw;
  height: 8vh;
  font-size: 3vh;
  margin-left: 2vw;
}

h1 {
  color: rgb(0, 0, 0);
  margin-right: 1000px;
  margin-bottom: 50px;
}
h2 {
  color: rgb(24, 22, 22);
  font-size: 22px;
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
  width: auto;
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
