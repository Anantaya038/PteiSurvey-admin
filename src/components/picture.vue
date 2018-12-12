<template>
    <div class="pre">
      <b-card>
        <div>  
            <h2>Input your question</h2>
            <b-form-input class="input" type="text" v-model="newText" placeholder="Input your question ..." ></b-form-input><br>
            <h2>Input your Choice</h2>
            <input type="text" class="input2" v-model="newchoice" placeholder="Add Choice ...">
        </div>
        <img :src="imagepreview" width="150" height="125" class="preview-image" v-on:click="openupload()" 
            alt="Responsive image" />

        <input type="file" id="file-filed" @change="previewFile" />

        <b-button class="buttonCSS3" @click="add">Add</b-button><br>
        <div class="imm" v-for="img in this.url2" :key="img" >
    
          <img :src="img" />
        </div>
         

        <b-radio  v-for="ch in this.newchoices" :key="ch" class="input5" id="radio" ><h2>{{ch}}</h2></b-radio>

      
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
</template>


<script>
import { firestore } from "../firebase.js";
import firebase from "firebase";

export default {
  data() {
    return {
      newText: "",
      id: "",
      surveys: [],
      image: [],
      imagepreview: require("../photo/picc.png"),
      pic: [],
      someData: null,
      url:null,
      url2: [],
      newchoices: [], // radio
      newchoice: "", //text
    };
  },

  firestore() {
    return {
      surveys: firestore.collection("surveys"),
      pic: firestore.collection("picture")
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
          option: this.newchoices[i],
          url: this.url2[i]
        };
        newdatas.push(newdata);
      }


      this.$firestore.surveys
        .doc()
        .set({ qid: id, qname: this.newText, type: "qimg" , ans: newdatas });
    },

    previewFile(event) {
      this.someData = event.target.files[0];
      //this.add(this.someData);
    },

    add() {
      this.newchoices.push(this.newchoice);
      

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

    openupload() {
      document.getElementById("file-filed").click();
    },
    
  }
};
// console.log('upload picture complete');

      // upload.on('state_changed' ,
      // function(snapshot){

      //   var uu = upload.snapshot.downloadURL;
      //   console.log(uu);

      // },
      // function(error){

      // },
      // function () {
      //    var url = upload.snapshot.downloadURL;

      // });

      // var storageRef = firebase.storage().ref();
      // var mountainImagesRef = storageRef.child("/images/newfile.jpg");

      // storageRef.put(file).then(function(snapshot) {
      //   console.log("Uploaded a blob or file!");
      // });
</script>

<style scoped>
.imm{
  margin-left: 70vh;
}
.input5 {
  width: 70vw;
  height: 11vh;
  font-size: 18px;
  margin-top: 2vh;
  margin-bottom: -15vh;
}
h2{
  font-size: 21px;
}
.preview-image{
  margin-left: 52vh;
}
.marginTop {
  margin-top: 7vh;
}
p {
  color: black;
}
.input2 {
  width: 40vw;
  height: 8vh;
  font-size: 20px;
  margin-left: 50vh;
}
img{
   width: 20vh;
  height: 20vh;
  margin: 1vh;
  border-style:inset;
  border-width: 1.5px;
}
.buttonCSS3 {
  background-color: Orange;
  width: 10vw;
  height: 8vh;
  font-size: 3vh;
}

.input {
   width: 92vw;
  height:10vh;
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
.buttonCSS2{
   background-color: red;
  width: 10vw;
  height: 8vh;
  font-size: 3.5vh;
  text-align: center;
}

.button1 {
  background-color: yellowgreen;
  border-radius: 20px;
  width: 18vw;
  height: 30vh;
  font-size: 3.5vh;

  margin-top: 70px;
  margin-right: 70px;
  margin-bottom: 50px;
  margin-left: 80px;
}
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
.qw {
  color: white;
}

h2{
  color: rgb(0, 0, 0);
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
