<template>
  <div id="app">
    <div id="logo">
      <h1>
        <strong><i><u>Actual</u></i> tiny 1px icons </strong>
      </h1>
    </div>
    <div id="cpAlert">
      <p id="cpText">
        Copied!
      </p>
    </div>
    <Designer v-on:copiedData="copyAlert()"/>
    <div id="showcase">
      <Showcase v-on:copiedData="copyAlert()"/>
    </div>
<footer>
  <p><a href=https://sean-fischer.mit-license.org target="_blank">MIT</a> - <a href=https://github.com/fischersean/actualteenyicons.com target="_blank">Source</a></p> 
  <p><b>Made with ❤️  by <a href=https://github.com/fischersean target="_blank">Sean Fischer </a> </b></p> 
  <p>This is a joke</p>
</footer>
  </div>

</template>

<script>
import Showcase from './components/Showcase';
import Designer from './components/Designer';
export default {
  name: 'App',
  components: {
    Designer,
    Showcase,
  },
  methods: {
    copyAlert: function(){
      var al = document.getElementById("cpAlert")
      al.classList.add("popup");
      al.addEventListener("animationend", function(){
        al.classList.remove("popup");
      }, false)
    },
  },
};
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Covered+By+Your+Grace&display=swap');
@import url('https://fonts.googleapis.com/css2?family=Source+Code+Pro&display=swap');
@keyframes popup {
  0%   {bottom: -100px;}
  50%  {bottom: 100px;}
  75%  {bottom: 100px;}
  100% {bottom: -100px;}
}
#logo{
    font-family: 'Covered By Your Grace', cursive;
    letter-spacing: 2px;
    font-size: x-large;
    margin: auto;
}
#app {
  display: flex;
  flex-direction: column;
  font-family: 'Source Code Pro', monospace;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 20px;
  /*max-width: 70em;;*/
  margin: auto;
}
#cpAlert{
  position: fixed;
  bottom: -100px;
  left: 50%;
  transform: translate(-50%, -50%);
}
.popup {
  animation-name: popup;
  animation-duration: 0.75s;
}
#cpText{
  margin: auto;
  background: white;
  border-style: solid;
  border-color: black;
  padding: 0.75em;
  width: 5em;
  font-size: large;
  border-radius: 50px;
}
</style>
