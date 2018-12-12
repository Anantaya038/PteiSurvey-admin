<template>
    <div class="pre">
      <b-card>
        <h1>Question{{question.qid}}</h1>
        <div class="row">
            <b-form-input class="input" type="text" v-model="question.qname" placeholder="Input your question ..." ></b-form-input>
            
            </div><br>
            <input type="text" class="input2" v-model="newchoice" placeholder="Add Choice ..."><br>
        
        <img :src="imagepreview"  width="150" height="125" class="preview-image" v-on:click="openupload()" 
            alt="Responsive image" />
            

        <input type="file" id="file-filed" @change="previewFile" />
        <!-- <img :src="url" v-for="img in this.url2" :key="img"/>  -->

        <b-button class="buttonCSS3" @click="add">Add</b-button><br><br><br>

        <div class="eee">
        <div v-for="q in this.question.ans" :key="q.url">
            <img :src="q.url" /> 
            <b-radio name="choice" class="input5" id="radio" ><h4>
        {{q.option}}</h4></b-radio>
        </div>
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
                    <b-button class="buttonCSS4" >Back</b-button> 
                </router-link>
        </div>   
    </div>
</template>


<script>
import { firestore } from "../firebase.js";
import firebase from "firebase";

export default {
  props: ["question"],
  data() {
    return {
      newText: "",
      id: "",
      surveys: [],
      image: [],
      imagepreview: require("../photo/picc.png"),
      pic: [],
      someData: null,
      url: null,
      url2: [],
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
        qname: this.question.qname,
        type: "qimg",
        ans: this.question.ans
      });
    },
    add() {
        
     var filename = this.someData.name;
      var storageRef = firebase.storage().ref("img/" + filename);
      //var upload = storageRef.put(this.someData);
      var parent = this;
      storageRef.put(this.someData).then(function(snapshot) {
        console.log("Uploaded a blob or file!");

        snapshot.ref.getDownloadURL().then(function(downloadURL) {
          //console.log("File available at", downloadURL);
          //console.log(downloadURL);
          parent.show(downloadURL);
          
        });
      });
      console.log(this.newchoice);
      this.question.ans.push({
        option: this.newchoice,
        url: this.url2
      });
      console.log(this.newchoices);
    },
    show(downloadURL){
      console.log(downloadURL);
      //this.imagepreview= require(downloadURL);
      this.url = downloadURL;
      this.puturl();
      
    },
    puturl(){
      this.url2.push(this.url);
    },
    cancel(key) {
      this.$firestore.surveys.doc(key).delete();
    },
    previewFile(event) {
      this.someData = event.target.files[0];
      //this.add(this.someData);
    },
    openupload() {
      document.getElementById("file-filed").click();
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
.preview-image{
  margin-left: 52vh;
}
.input5 {
  width: 70vw;
  height: 11vh;
  font-size: 21px;
  margin-top: 2vh;
}
.eee{
  margin-left: 20vh;
}
h4{
  color: black;
}
img{
  width: 20vh;
  height: 20vh;
  margin: 1vh;
  border-style:inset;
  border-width: 1.5px;
}
.buttonCSS3 {
  background-color:Orange;
  width: 7vw;
  height: 7vh;
  font-size: 3vh;
  margin-left: 50px;
}
p {
  color: black;
}
.input {
  width: 90vw;
  height: 11vh;
  font-size: 21px;
  margin-left: 2vw;
}
.input2 {
  width: 40vw;
  height: 7vh;
  font-size: 20px;
  margin-left: 50vh;
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
/* .button1 {
  background-color: yellowgreen;
  border-radius: 20px;
  width: 18vw;
  height: 30vh;
  font-size: 3.5vh;

  margin-top: 70px;
  margin-right: 70px;
  margin-bottom: 50px;
  margin-left: 80px;
} */
.button4 {
  background-color: inherit;
  border-radius: inherit;
  width: auto;
  height: auto;
  margin-top: 30px;
  margin-right: 70px;
  margin-bottom: 20px;
  margin-left: 80px;
}
h1 {
  color: rgb(2, 2, 2);
}
.img-body {
  height: 30vh;
  width: 30vh;
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
