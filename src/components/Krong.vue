<template>
    <div class="fullscreen">
      <b-navbar toggleable="md" variant="color">
  <b-navbar-brand><h2><b>PTEI Survey</b></h2></b-navbar-brand>
  <b-collapse is-nav id="nav_collapse">
    <!-- Right aligned nav items -->
    <b-navbar-nav class="ml-auto">
       <b-nav-item href="#/adsurveydesign">Survey Designer</b-nav-item>

        <b-nav-item-dropdown text="View Data" right>
        <b-dropdown-item href="#/adviewdata">Tourist</b-dropdown-item>
        <b-dropdown-item href="#/showq">Question</b-dropdown-item>
        <b-dropdown-item href="#/allview">All</b-dropdown-item>
        </b-nav-item-dropdown>
    </b-navbar-nav>
    <b-navbar-nav class="ml-auto">
      <p>{{currentUsersh}}</p>
      <b-nav-item-dropdown right>
        <!-- Using button-content slot -->
        <template slot="button-content">
                  
          <em><b-img style="width:3vw;" :src="require('../photo/register.png')"></b-img></em>
        </template>
        <b-dropdown-item v-on:click="home"><b-img style="width:3vw;" src="https://firebasestorage.googleapis.com/v0/b/ptei-1c8c4.appspot.com/o/photo%2Fhome.png?alt=media&token=84d8e84a-4efa-4108-ab73-afff18327156"></b-img><b>Home</b> </b-dropdown-item>
        <b-dropdown-item v-on:click="logout"><b-img style="width:3vw;" src="https://firebasestorage.googleapis.com/v0/b/ptei-1c8c4.appspot.com/o/photo%2Flogout.png?alt=media&token=6825d9f8-6736-478f-a313-60edcf5c1ba5"></b-img><b>Signout</b> </b-dropdown-item>
      </b-nav-item-dropdown>
    </b-navbar-nav>

  </b-collapse>
</b-navbar>
<router-view></router-view>
</div>
</template>

<script>
import firebase from 'firebase';
export default {

   data () {
        return {
            currentUsersh: firebase.auth().currentUser.email,

            isLoggedIn: false,
            currentUser: false
        }
    }, 
    methods:{
        logout(){
            firebase.auth().signOut().then(() => {
                this.$router.push('/adminlogin');
                alert('Log out');
            });
        },
        register(){
            this.$router.push('/register');
        },
        home(){
          this.$router.push('/adminhome');
        }
    }
}
</script>


<style>
.fullscreen {
  height: 100vh;
  width: 100%;
  background-color: rgb(255, 255, 255);

}
.navbar {
  background-color: #193c6c;
}
h2{
  color: white;
}
.navbar-light .navbar-nav .nav-link {
  color: white;
}
p{
  color: white;
}
</style>
