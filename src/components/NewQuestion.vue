<template>
    <div class="pre">

        <!-- <router-link to="/adsurveydesign">
                <b-button class="button1">  <b-img :src="require('../photo/b.png')" class="img-body2"></b-img></b-button>
        </router-link> -->
        
        <h1>Pick & Choose</h1>
        <div class="center">
            <router-link to="/choice" class="col">
                <b-button class="buttonCSS" >Multiple choices</b-button>            
            </router-link>     

            <router-link to="/picture" class="col">
                <b-button class="buttonCSS" >Picture</b-button>
            </router-link> 
        </div>
        <div class="center">
            <!-- v-on:click="text()" -->
            <router-link to="/text" class="col">
                <b-button class="buttonCSS" >Text input</b-button>
            </router-link>   
            <router-link to="/yesno" class="col">
                <b-button class="buttonCSS" >Yes or No</b-button>
            </router-link> 
        </div>
        <div class="center">
            <router-link to="/satisfaction" class="col">
            <b-button class="buttonCSS">Satisfaction</b-button>
            </router-link>   
            <router-link to="/opinion" class="col">
            <b-button class="buttonCSS" >Opinion</b-button>
            </router-link> 
        </div>
        <div class="center">
            <router-link to="/expect" class="col">
            <b-button class="buttonCSS" >Expect</b-button>
            </router-link> 
            <router-link to="/radio" class="col">
            <b-button class="buttonCSS" >Radio</b-button>
            </router-link> 
        </div>
        <div class="center">
            <router-link to="/expend" class="col">
            <b-button class="buttonCSS" >Expend</b-button>
            </router-link>
        </div>
            

    </div>
</template>

<script>
import {firestore} from '../firebase.js'

export default {

     data (){
        return{
            surveys:[],
            id:''
        }
    },
    firestore (){
        return {
            surveys : firestore.collection('surveys')
        }
    },
    // methods:{
    //     choice(){
    //         var length = this.surveys.length+1;
    //         var newQ = 'q'+length++;
    //         var id = length-1;
    //         console.log(newQ);
    //         console.log(id);
    //         this.$firestore.surveys.doc(newQ).set({qid:id});
    //     },
    //     picture(){
    //         var length = this.surveys.length+1;
    //         var newQ = 'q'+length++;
    //         var id = length-1;
    //         console.log(newQ);
    //         console.log(id);
    //         this.$firestore.surveys.doc(newQ).set({qid:id});
    //     },
    //     text(){
    //         var length = this.surveys.length+1;
    //         var newQ = 'q'+length++;
    //         var id = length-1;
    //         console.log(newQ);
    //         console.log(id);
    //         this.$firestore.surveys.doc(newQ).set({qid:id});
    //     },
    //     yesno(){
    //         var length = this.surveys.length+1;
    //         var newQ = 'q'+length++;
    //         var id = length-1;
    //         console.log(newQ);
    //         console.log(id);
    //         this.$firestore.surveys.doc(newQ).set({qid:id});
    //     },
    //     satisfaction(){
    //         var length = this.surveys.length+1;
    //         var newQ = 'q'+length++;
    //         var id = length-1;
    //         console.log(newQ);
    //         console.log(id);
    //         this.$firestore.surveys.doc(newQ).set({qid:id});
    //     },
    //     opinion(){
    //         var length = this.surveys.length+1;
    //         var newQ = 'q'+length++;
    //         var id = length-1;
    //         console.log(newQ);
    //         console.log(id);
    //         this.$firestore.surveys.doc(newQ).set({qid:id});
    //     }
    // }
}
</script>


<style scoped>
h1{
    color: rgb(0, 0, 0);
}
.center{
    text-align: center;
}
.pre{
margin-top: 2vh;
margin-left: 2vw;
margin-right: 2vw;
margin-block-end: 2vh;
}
.btn{
    margin-top: 3vh;
        width: 30vw;
        height: 7vh;
}
</style>
