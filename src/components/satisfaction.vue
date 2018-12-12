<template>
    <div class="pre">
      <b-card>
        <h2>Input your title</h2>
        <div>
            <b-form-input class="input" type="text" v-model="inputtitle" placeholder="Input your title ..." ></b-form-input><br>              
        </div> 
        <div> 
            <input type="text" class="input2" v-model="newInput" placeholder="Input ...">

            <b-button class="button1">  <b-img :src="require('../photo/s1.png')" class="img-body"></b-img></b-button>
            <b-button class="button1">  <b-img :src="require('../photo/s2.png')" class="img-body"></b-img></b-button>
            <b-button class="button1">  <b-img :src="require('../photo/s3.png')" class="img-body"></b-img></b-button>
            <b-button class="button1">  <b-img :src="require('../photo/s4.png')" class="img-body"></b-img></b-button>       
            <b-button class="button1">  <b-img :src="require('../photo/s5.png')" class="img-body"></b-img></b-button><br><br>
        </div>  
        <div> 
             <input type="text" class="input2" v-model="newInput2" placeholder="Input ...">

            <b-button class="button1">  <b-img :src="require('../photo/s1.png')" class="img-body"></b-img></b-button>
            <b-button class="button1">  <b-img :src="require('../photo/s2.png')" class="img-body"></b-img></b-button>
            <b-button class="button1">  <b-img :src="require('../photo/s3.png')" class="img-body"></b-img></b-button>
            <b-button class="button1">  <b-img :src="require('../photo/s4.png')" class="img-body"></b-img></b-button>       
            <b-button class="button1">  <b-img :src="require('../photo/s5.png')" class="img-body"></b-img></b-button>
        </div><br>
        <div>
            <input type="text" class="input9" v-model="newchoice" placeholder="Add question satisfaction ...">
            
            <b-button class="buttonCSS3" v-on:click="add()">Add</b-button>
                
            <b-radio name="choice" v-for="ch in this.newchoices" :key="ch" class="input5" id="radio" >{{ch}}</b-radio>
            
        </div>
        </b-card>
       
        <div class="row">
            <router-link class="col" to="/newquestion">
                <b-button class="buttonCSS" v-on:click="save()">Save</b-button>
            </router-link>

            <router-link class="col" to="/newquestion">
                <b-button class="buttonCSS2" >Cancel</b-button>    
            </router-link>  
        </div>
    </div>
    <!-- <div style="margin: auto; margin-top: 10vh">
        <h1>PTEI Survey</h1>
        <div>
            <b-form-input class="input" type="text" v-model="inputtitle" placeholder="Input your title ..." ></b-form-input><br>
            <b-form-input class="input" type="text" v-model="newText" placeholder="Input your question ..." ></b-form-input><br>              
        </div> 
        <div> 
            <input type="text" class="input2" v-model="newInput" placeholder="Input ...">

            <b-button class="button1">  <b-img :src="require('../photo/s1.png')" class="img-body"></b-img></b-button>
            <b-button class="button1">  <b-img :src="require('../photo/s2.png')" class="img-body"></b-img></b-button>
            <b-button class="button1">  <b-img :src="require('../photo/s3.png')" class="img-body"></b-img></b-button>
            <b-button class="button1">  <b-img :src="require('../photo/s4.png')" class="img-body"></b-img></b-button>       
            <b-button class="button1">  <b-img :src="require('../photo/s5.png')" class="img-body"></b-img></b-button><br><br>

        </div>  
        <div> 
             <input type="text" class="input2" v-model="newInput2" placeholder="Input ...">

            <b-button class="button1">  <b-img :src="require('../photo/s1.png')" class="img-body"></b-img></b-button>
            <b-button class="button1">  <b-img :src="require('../photo/s2.png')" class="img-body"></b-img></b-button>
            <b-button class="button1">  <b-img :src="require('../photo/s3.png')" class="img-body"></b-img></b-button>
            <b-button class="button1">  <b-img :src="require('../photo/s4.png')" class="img-body"></b-img></b-button>       
            <b-button class="button1">  <b-img :src="require('../photo/s5.png')" class="img-body"></b-img></b-button>
        </div>
        <div>
            <router-link class="qw" to="/newquestion">
                <b-button class="buttonCSS" v-on:click="save()">Save</b-button>
            </router-link>

            <router-link class="qw" to="/newquestion">
                <b-button class="buttonCSS2" >Cancel</b-button>    
            </router-link>  
        </div>
    </div> -->
     
</template>


<script>
import { firestore } from "../firebase.js";

export default {
  data() {
    return {
      newText: "",
      id: "",
      newInput: "",
      newInput2: "",
      surveys: [],
      inputtitle: "",
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
    save() {
      console.log(this.newText);
      var length = this.surveys.length + 1;
      var newQ = "q" + length;
      var id = length++;
      console.log(newQ);
      console.log(id);

      var newdatas = [];
      for (var i = 0; i < this.newchoices.length; i++) {
        var newdata = {
          option: this.newchoices[i]
        };
        newdatas.push(newdata);
      }

      this.$firestore.surveys.doc().set({
        qid: id,
        qsub: newdatas,
        type: "qsatisfaction",
        qtitle: this.inputtitle,
        titleBe: this.newInput,
        titleAf: this.newInput2
      });
    },
    add() {
      console.log(this.newchoice);
      this.newchoices.push(this.newchoice);
      console.log(this.newchoices);
    }

    // cancel(){
    //     var length = this.surveys.length;
    //     var newQ = 'q'+length;

    //     this.$firestore.surveys.doc(newQ).delete()
    // }
  }
};
</script>


<style scoped>
.input5 {
  width: 70vw;
  height: 11vh;
  font-size: 21px;
  margin-top: 2vh;
  margin-bottom: -15vh;
  margin-left: 40vh;
}
.input2 {
  width: 35vw;
  height: 8vh;
  font-size: 20px;
  margin-left: 12vh;
}
.input9 {
  width: 35vw;
  height: 8vh;
  font-size: 20px;
  margin-left: 50vh;
}
.qw {
  color: rgb(0, 0, 0);
}
p {
  color: black;
}
.input {
  width: 70vw;
  height: 11vh;
  font-size: 20px;
}
.center {
  width: 37vw;
  height: 8.5vh;
  margin: auto;
  border: 3px;
  padding: 10px;
}

.buttonCSS {
  width: 10vw;
  height: 8vh;
  font-size: 3.5vh;
  text-align: center;
}
.buttonCSS2 {
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
  margin-left: 25px;
}
.button1 {
  background-color: inherit;
  border-radius: inherit;
  width: auto;
  height: auto;

  border-radius: 50%;

  margin-top: 5px;
  margin-right: 5px;
  margin-bottom: 5px;
  margin-left: 5px;
}
.input{
  width: 92vw;
  height:10vh;
  font-size: 20px;
}
h2 {
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
  width: 80vw;
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
