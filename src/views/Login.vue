<template>
  
  <div class="container-login">
    <div class="logo-login">
      <img class="image-logo" src="../assets/logo.png" alt="">
    </div>
    <div class="inputs">
      <input class="input-username" type="text" placeholder="Username">
      <input class="input-password" type="text" placeholder="Password">
    </div>
    <div class="same-line1">
      <div class="remember-chbox">
        <input type="checkbox" id="chbox" name="chbox">
        <label for="chbox">Remember Me</label>
      </div>
      <div class="forgot-password">
        <label>Forgot Password?</label>
      </div>
    </div>
    <div class="login">
      <button class="login-btn" @click="goToDashboard">LOGIN</button>
    </div>
    <div class="same-line2">
      <div class="hr1"><hr></div>
      <div class="or">or</div>
      <div class="hr2"><hr></div>
    </div>
    <div class="login-google">
      <button class="login-google-btn">Log in with Google</button>
    </div>
    <div class="login-facebook">
      <button class="login-facebook-btn">Log in with Facebook</button>
    </div>
    <div class="signin">
      <label class="signin-lbl">Don't have an account? Sign in</label>
    </div>
  </div>

</template>

<script lang="ts">
import '../assets/css/Login/app.css';
import { defineComponent } from 'vue';
import { useRouter } from 'vue-router';


export default defineComponent({
  name: 'PageOne',
  setup() {
     const router = useRouter();
    
     const goToDashboard = () => {
       router.push({ name: 'Dashboard' });
     };
    
     return { goToDashboard };
  }
});
</script>

<style>
body{
  background-color: rgb(73, 89, 105);
}
</style>