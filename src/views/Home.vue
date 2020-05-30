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
        <div id="passGroup"> <!-- Nisam bio siguran kako bez diva da napravim ovo-->
          <label for="pass">Password</label>
          <button @click="changeVisibility" id="eyeBtn"><i v-bind:class="eye"></i></button>
        </div> <!-- precica za pozivanje metode sa @, sv je sta koristis al praksa je v- za sve sto je vue -->
        <input id="pass" v-model="inputPass" v-bind:type="visible" > <!-- bilo koji html atribut moze da se poveze sa nekim data elementom -->
        <div v-if="hasError">{{error}}</div>
        <button v-on:click="validate" id="loginBtn">Log in</button>
        <!-- {{visible}} -->
      </div>
    </div>
    <HelloWorld msg="Welcome to Your Vue.js App"/>
    <p>1. email: <u>basic@basic.com</u> | pass: <u>secret</u></p>
    <p>2. email: <u>admin@admin.com</u> | pass: <u>secret</u></p>
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
      email: 'basic@basic.com',
      pass:'secret',
      adminEmail:'admin@admin.com',
      adminPass:'secret',
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
        this.$router.push({path: '/basic_user'}) //ovim definises na koji view da te posalje. Mora this jer nije pozvan na ovom elementu. Mora ovako
        alert('Validation successful');
      } else if(this.inputEmail === this.adminEmail && this.inputPass === this.adminPass){
        this.$router.push({path: '/admin'}) //ovim definises na koji view da te posalje. Mora this jer nije pozvan na ovom elementu. Mora ovako
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
      //border:1px solid red;
      display:flex;
      flex-direction: row;
      justify-content: space-between;
      align-items: center; //beware of this for the left box
      transition: 1s width;
      .left {
        //border:1px solid green;
        background-color: #fff;
        box-shadow: 0 0 3px #333;
        display: flex;
        justify-content: center;
        flex-direction: column;
        width:50%;
        height:160px;
        text-align: left;
        transition: 1s height;
        h3 {
          margin:0;
          padding:0 30px;
        }
        p {
          margin:0;
          padding:15px 30px 0 30px;
        }
      }
      .right {
        //border:1px solid green;
        border-radius: 5px;
        box-shadow: 0 0 20px;
        width:50%;
        height:280px; 
        text-align: left;
        background-color:#32475C;
        color:#abb8c3;
        transition: 1s height;
        input {
          display:block;
          background-color:#32475C;
          width:69%; //zasto ovde ide 69 %, iako je ostalo sve 70% ?
          margin: 0 auto;
          padding:10px 10px;
          color:#fff;
          border:none;
          outline:none;
          box-shadow: 0px 0px 3px rgb(69, 97, 126); //kako ovo ?
          transition: 0.3s box-shadow;
          &:hover{
            box-shadow: 0px 0px 5px rgb(95, 134, 173);
          }
          &:focus, &:active {
            outline:none;
            background-color:#32475C;
            box-shadow: 0px 0px 6px 0px;
          }
          &:-webkit-autofill, &:-webkit-autofill:hover, &:-webkit-autofill:focus { //still an issue on autocomplete
          border: none;
          -webkit-text-fill-color: red;
          -webkit-input-fill-background-color:red;
          //-webkit-box-shadow: none;
          }
        }
        label{
          &[for="email"] {
          display:block;
          // border:1px solid orange;
          margin:40px auto 0 auto;
          width:75%;
          }
          &[for="pass"] {
            display:inline;
            // border:1px solid orange;
          }
          &:hover {
            cursor: pointer;
          }
        }
        div { //warning message
          width:75%;
          margin: 0 auto;
          &#passGroup { //password + eye button
          margin:15px auto 0 auto;
          width:75%;
          }
        }
        button {
          transition: 0.4s box-shadow;
          &#eyeBtn {
            color:#fff;
            background-color:rgba(0,0,0,0);
            border:none;
            outline:none;
            border-radius: 50%;
            &:hover {
              box-shadow: 0px 0px 5px rgb(95, 134, 173);
            }
          }
          &#loginBtn { //id za login dugme
            display:block;
            width:75%;
            margin: 25px auto 0 auto;
            padding: 15px 0;
            &:hover {
              box-shadow: 0px 0px 5px #fff;
            }
          }
          &:hover {
            cursor:pointer;
          }
        }
      }
    }
  }
  @media only screen and (max-width: 860px) { 
  .home {
    .for {
      width:80%;
      transition:1s width;
      .right {
        height:300px;
        transition: 1s height;
      }
      .left {
        height:200px;
        transition: 1s height;
      }
    }
  }
}
  @media only screen and (max-width: 673px) {
  .home {
    .for {
      width:95%;
      transition:1s width;
      .right {
        height:300px;
        transition: 1s height;
      }
      .left {
        height:200px;
        transition: 1s height;
      }
    }
  }
}

</style>
