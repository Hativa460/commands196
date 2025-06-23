<template>
    <div id="end-page">
        <p id="txt" >סיימנו!</p>
         <p id="txt2">שנתרגל שוב?</p>
        <img id="restart" src="../assets/media/restart.svg" alt="restart" class="animate__animated animate__rotateIn" @click="restart">
    </div>
  </template>
  
  <script>
  
  export default {
    name: "end-page",
    props: [""],
    data() {
      return {};
    },
    // mounted() {
    //   this.startConfetti();
    // },
    methods: {
        restart() {
            this.$emit('restart');
        }
    //   startConfetti() {
    //     const duration = 2 * 1000; // 4 seconds
    //     const end = Date.now() + duration;
  
    //     const confettiSettings = {
    //       angle: 90, // Horizontal direction
    //       spread: 360, // Full circle spread
    //       origin: { x: 0.5, y: 0.5 }, // Center of the screen
    //       colors: ['#EEDADA'], // Confetti color
    //       particleCount: 200, // Number of confetti pieces
    //       gravity: 0.5, // Slight downward movement
    //       ticks: 150 // Speed of confetti fall
    //     };
  
    //     const interval = setInterval(() => {
    //       if (Date.now() > end) {
    //         clearInterval(interval);
    //       }
    //       confetti(confettiSettings);
    //     }, 750); // Fire confetti every 100 ms
    //   },
    },
  };
  </script>
  
  <style scoped>
  #final-page {
    margin: 0;
    overflow-x: hidden;
    height: 100%;
    width: 100vw;
    position: absolute;
    top: 0;
    right: 0;
  }

  #txt {
    font-family: "asakim";
    font-size: 5rem;
    margin: auto;
    text-align: center;
    margin-top: 70%;
    color: #f6f7e8;
    text-shadow: 10px -2px 10px rgba(0, 0, 0, 0.5);
    animation: backInDown;
    animation-duration: 1s;
  }

    #txt2 {
    font-family: "asakim";
    font-size: 4rem;
    margin: auto;
    text-align: center;
    margin-top: 10%;
    color: #f6f7e8;
    text-shadow: 10px -2px 10px rgba(0, 0, 0, 0.5);
    animation:backInUp ;
    animation-duration: 1s;
  }
  
  #restart {
    display: block;
    margin: auto;
    margin-top: 5%;
    max-width: 100%;
    height: 15vh;
  }
  </style>
  