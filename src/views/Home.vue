<template>
  <div class="home">
    <div class="for">
      <div class="left">
        <h3>Login</h3>
        <p>Lorem ipsum dolor, sit amet consectetur adipisicing elit. Asperiores, qui.</p>
      </div>
      <div class="right">
        <label for="email">Email</label>
        <input id="email" v-model="inputEmail" type="text">
        <label for="pass">Password</label><button @click="changeVisibility" id="eyeBtn"><i v-bind:class="eye"></i></button> <!-- precica za pozivanje metode sa @, sv je sta koristis al praksa je v- za sve sto je vue -->
        <input id="pass" v-model="inputPass" v-bind:type="visible" > <!-- bilo koji html atribut moze da se poveze sa nekim data elementom -->
        <div v-if="hasError">{{error}}</div>
        <button v-on:click="validate" id="loginBtn">Login</button>
        <!-- {{visible}} -->
      </div>
    </div>
    <HelloWorld msg="Welcome to Your Vue.js App"/>
  </div>
</template>

<script>
// @ is an alias to /src
import HelloWorld from '@/components/HelloWorld.vue'

export default {
  name: 'Home',
  components: {
    HelloWorld
  },
  data: function(){ //ubacis ovde ovako da vracas data
    return {
      email: 'nikola@nikola.com',
      pass:'secret',
      inputEmail:'',
      inputPass:'',
      visible: 'password',
      eye: 'fas fa-eye',
      error:'The credentials are not correct.',
      hasError: false
    }
  },
  methods: {
    changeVisibility: function(){
      if(this.visible === 'password'){
        this.visible = 'text';
        this.eye = 'fas fa-eye-slash';
      } else {
        this.visible = 'password';
        this.eye = 'fas fa-eye';
      }
    },
    validate: function(){
      if(this.inputEmail === this.email && this.inputPass === this.pass){
        //this.hasError = false;
        this.$router.push({path: '/about'}) //ovim definises na koji view da te posalje. Mora this jer nije pozvan na ovom elementu. Mora ovako
        alert('Validation successful');
      } else {
        this.hasError = true;
      }
    }
  }
}
</script>
<style lang="scss" scoped> //ako pise scoped, onda je vezano samo za sve sto je za ovu komponentu
  .home{
    .for {
      width:50%;
      margin: 0 auto;
      border:1px solid red;
      display:flex;
      flex-direction: row;
      justify-content: space-between;
      align-items: center; //beware of this for the left box
      .left {
        border:1px solid green;
        width:50%;
        text-align: left;
        h3 {
          margin:0;
          padding:0;
        }
        p {
          margin:0;
          padding:0;
        }
      }
      .right {
        border:1px solid green;
        width:50%;
        text-align: left;
        background-color:#32475C;
        color:#abb8c3;
        input {
          display:block;
          background-color:#32475C;
          color:#fff;
          border:none;
          outline:none;
          box-shadow: 0px 0px 3px 0px; //kako ovo ?
          
          &:focus, &:active {
            outline:none;
            background-color:#32475C;
            box-shadow: 0px 0px 6px 0px;
          }
          &:-webkit-autofill, &:-webkit-autofill:hover, &:-webkit-autofill:focus { //still an issue on autocomplete
          border: none;
          -webkit-text-fill-color: red;
          -webkit-input-fill-background-color:red;
          -webkit-box-shadow: none;
          }
        }
        label{
          &[for="email"] {
          display:block;
          // border:1px solid orange;
          margin:0;
          }
          &[for="pass"] {
            display:inline;
            // width:30%;
            // border:1px solid orange;
          }
        }
        button {
          &#eyeBtn {
            color:#fff;
            background-color:rgba(0,0,0,0);
            border:none;
            outline:none;
          }
          &#loginBtn { //id za login dugme
            display:block;
            width:80%;
          }
          &:hover {
            cursor:pointer;
          }
        }
      }
    }
  }
</style>
