<template>
    <div class="pre">
        <b-card>
        <h2>Input your question</h2>
        <div>
            <b-form-input class="input" type="text" v-model="newText" placeholder="Input your question ..." ></b-form-input><br>
        <div class="row">
             <div class="col"><b-img  :src="require('../photo/y2.png')" class="img-body"></b-img></div>
            <div class="col"><b-img :src="require('../photo/no2.png')" class="img-body"></b-img></div>
       </div>
                 
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
</template>


<script>
import {firestore} from '../firebase.js'

export default {

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
        save(){
            // console.log(this.newText);
            // var length = this.surveys.length;
            // var newQ = 'q'+length;
            // var id = length;
            // console.log(newQ);
            // console.log(id);
            console.log(this.newText);
            var length = this.surveys.length+1;
            var newQ = 'q'+length;
            var id = length++;
            console.log(newQ);
            console.log(id);
            
            this.$firestore.surveys.doc().set({qid:id,qname:this.newText,type:"q-yes-no"})
        },
        // cancel(){
        //     var length = this.surveys.length;
        //     var newQ = 'q'+length;

        //     this.$firestore.surveys.doc(newQ).delete()
        // }
    }
}
</script>


<style scoped>
.pre{
margin-top: 4vh;
margin-left: 2vw;
margin-right: 2vw;
margin-block-end: 2vh;
}
.qw {
    color: rgb(0, 0, 0);
}
p{
    color: black;
}
.input{
     width: 92vw;
  height:10vh;
  font-size: 20px;
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
.img-body {
  height: 25vh;
  width: 25vh;
}
.card-body{
  width: 80vw;
  height:70vh;
  text-align: left;
}
.col{
  text-align: center;
  margin-left: 20vh;
}
.row{
  margin-top: 2vh;
  text-align: center;
}
h2{
    color: black;
}
</style>
