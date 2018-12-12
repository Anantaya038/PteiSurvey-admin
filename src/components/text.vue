<template>
    <div class="pre">
        <b-card>
        <h2>Input your question</h2><br>
        <div>
                <b-form-input class="input" type="text" v-model="newText" placeholder="Input your question ..." ></b-form-input><br>  
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
    //props:['question'],
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
            console.log(this.newText);
            var length = this.surveys.length+1;
            var newQ = 'q'+length;
            var id = length++;
            console.log(newQ);
            console.log(id);
            
            this.$firestore.surveys.doc().set({qid:id,qname:this.newText,type:"qtextinput"})
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
  height: 20vh;
}
h2 {
  color: rgb(24, 22, 22);
}
.pre{
margin-top: 4vh;
margin-left: 2vw;
margin-right: 2vw;
margin-block-end: 2vh;
}
.card-body{
  width: 80vw;
  height:40vh;
  text-align: left;
}
.col{
  text-align: center;
}
.row{
  margin-top: 2vh;
}
</style>
