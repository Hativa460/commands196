<template>
  <div id="app">
        <div id="logos">
          <img class="logo" src="./assets/media/logo460.svg" alt="460">
          <img class="logo" id="logo196" src="./assets/media/196.png" alt="196">
        </div>
        <div>
          <img id="bgTank" src="./assets/media/backgroundTank.png" alt="bgTank">
        </div>
        <open-page v-if="page === 1" @next-page="nextPage"></open-page>
        <main-page v-if="page === 2" @next-page="nextPage"></main-page>
        <end-page v-if="page === 3" @restart="restart"></end-page>

  </div>
</template>
 
<script>
import OpenPage from "@/components/OpenPage";
import MainPage from "@/components/MainPage";
import EndPage from "@/components/EndPage";
export default {
  name: "app",
  components: {
    OpenPage,
    MainPage,
    EndPage
  },
    data() {
    return {
      page: 1,
    }
  },
    methods: {
    nextPage() {
      this.page ++;
      console.log(this.page);
    },
    restart(){
      this.page = 1;
    }
  }
};
</script>
<style>
* {
  user-select: none; 
  direction: rtl;
  /* overflow-x: hidden;
  -webkit-user-select: none; */
}
@font-face {
    font-family: "asakim";
    src: url("assets/fonts/asakim_bold-webfont.ttf");
}
@font-face {
  font-family: "assistant";
  src: url("./assets/fonts/Assistant-Regular.otf");
}
  body{
    margin: 0%;
    width: 100vw;
    height: 100%;
    background-color: #565252;
    /* overflow-x: hidden; */
  }
  #logos {
    position: fixed;
    top: 0%;
    left: 0%;
    z-index: 2;
    background-color: #565252;
    padding: 2%;
    width: 100%;
    display: flex;
    flex-wrap: nowrap;
    flex-direction: row-reverse;
    align-items: flex-end;
    justify-content: flex-start;
  }
  .logo {
    max-width: 100%;
    height: 8vh;
    margin-right: 4%;
  }
  #logo196 {
    margin-right: 0%;
  }
  #bgTank {
    position: absolute;
    top:40%;
    width: 55%;
    height: 55%;
  }
</style>