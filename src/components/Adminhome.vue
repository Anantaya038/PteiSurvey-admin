<template>
    <div style="margin: auto; margin-top: 28vh">
        <!-- <b-button class="button1" v-on:click="logout()">  <b-img :src="require('../photo/logout-icon.png')" class="img-body2"></b-img></b-button>
        
        <b-button class="button2" v-on:click="register()">  <b-img :src="require('../photo/register.png')" class="img-body2"></b-img></b-button>
         -->
        <div class="yy">
            <router-link to="/adsurveydesign">
                <b-button class="buttonCSS">Survey Designer</b-button>
            </router-link>            
        </div>
        <div >
            
            <b-button class="buttonCSS"><b-navbar-nav class="ml-auto">
            <b-nav-item-dropdown text="View Data" right>
            <b-dropdown-item href="#/adviewdata">Tourist</b-dropdown-item>
            <b-dropdown-item href="#/showq">Question</b-dropdown-item>
            <b-dropdown-item href="#/allview">All</b-dropdown-item>
            </b-nav-item-dropdown>
            </b-navbar-nav></b-button>
    
        </div>
    </div>
</template>

<script>
import firebase from "firebase";
export default {
  data() {
    return {
      currentUsersh: firebase.auth().currentUser.email,

      isLoggedIn: false,
      currentUser: false
    };
  },
  methods: {
    logout() {
      firebase
        .auth()
        .signOut()
        .then(() => {
          this.$router.push("/adminlogin");
          alert("Log out");
        });
    },
    register() {
      this.$router.push("/register");
    }
  }
};
</script>

<style scoped>
.yy {
  margin-top: -15vh;
}
.marginTop {
  margin-top: 7vh;
}
.img-body2 {
  width: 6vh;
  height: 6vh;
}
.buttonCSS {
  width: 35vh;
  height: 15vh;
  margin-left: 85vh;
  margin-top: 5vh;
  border-radius: 20px;
  font-size: 25px;
  color: #007bff;
  background-color: antiquewhite;
  
}

</style>
