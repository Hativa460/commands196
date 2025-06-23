<template>
  <div id="main-page" @touchstart="handleTouchStart" @touchend="handleTouchEnd">  
    <p id="title">פקודות צוות מרכבה</p>

    <transition
      :name="slideDirection"
      mode="out-in"
      @before-enter="beforeEnter"
      @after-enter="afterEnter"
    >
      <div
        class="card"
        :key="countSteps"
        :class="{ show: flipped }"
        @click="toggleFlip"
      >
        <div class="card-front titles">{{ currentTitle }}</div>
        <div class="card-back text">{{ currentInfo }}</div>
      </div>
    </transition>

    <div v-if="countSteps < titles.length" @click="nextCard" class="forwaedArrow"> </div>
    <div  v-if="countSteps > 1" @click="prevCard" class="backArrow"> </div>

    <div class="progress-wrapper">
      <div class="progress-label"></div>
      <EnergyProgressBar :progress="currentProgress" />
    </div>

     <div v-if="countSteps === titles.length" id="btn" @click="nextPage" class="animate__animated animate__slideInLeft toEndBtn">סיימתי</div>
    
  </div>
</template>

<script>
import json from "../../text.json";
import EnergyProgressBar from '../components/EnergyProgressBar.vue';

export default {
  name: "main-page",
  components: {
    EnergyProgressBar
  },
  data() {
    return {
      flipped: false,
      countSteps: 1,
      titles: json.cards[0].titles,
      info: json.cards[0].info,
      animating: false,
      touchStartX: 0,
      slideDirection: "slide-left"
    };
  },
  computed: {
    currentTitle() {
      return this.titles[this.countSteps - 1];
    },
    currentInfo() {
      return this.info[this.countSteps - 1];
    },
    currentProgress() {
      const total = this.titles.length-1;
      const step = this.countSteps-1;
      return Math.round((step / total) * 100);
    }
  },
  methods: {
    nextPage() {
        this.$emit('next-page');
    },
    toggleFlip() {
      this.flipped = !this.flipped;
    },
    nextCard() {
      if (this.animating || this.countSteps >= this.titles.length) return;
      if (this.flipped) {
        this.flipped = false;
        setTimeout(() => {
          this.slideDirection = "slide-left";
          this.countSteps++;
        }, 500);
      } else {
        this.slideDirection = "slide-left";
        this.countSteps++;
      }
    },
    prevCard() {
      if (this.animating || this.countSteps <= 1) return;

      if (this.flipped) {
        this.flipped = false;
        setTimeout(() => {
          this.slideDirection = "slide-right";
          this.countSteps--;
        }, 500);
      } else {
        this.slideDirection = "slide-right";
        this.countSteps--;
      }
    },
    beforeEnter() {
      this.animating = true;
    },
    afterEnter() {
      this.animating = false;
    },
    handleTouchStart(e) {
      this.touchStartX = e.changedTouches[0].clientX;
    },
    handleTouchEnd(e) {
      const touchEndX = e.changedTouches[0].clientX;
      const deltaX = touchEndX - this.touchStartX;

      if (Math.abs(deltaX) > 50 && !this.animating) {
        if (deltaX < 0) {
          this.nextCard();
        } else {
          this.prevCard();
        }
      }
    }
  }
};
</script>

<style scoped>
#main-page {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  width: 100vw;
  height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  overflow: hidden;
  flex-direction: column;
  z-index: 2;
}

#title {
    position: absolute;
    top:-1%;
    left: 40%;
    font-family: "asakim";
    font-size: 2rem;
    text-align: center;
    color: #f6f7e8;
    text-shadow: 10px -2px 10px rgba(0, 0, 0, 0.5);
    animation:fadeInRight ;
    animation-duration: 2s;
  }

.card {
  width: 70vw;
  height: 40vh;
  position: relative;
  perspective: 1000px;
  transform-style: preserve-3d;
  transition: rotate 500ms linear;
}

.card.show {
  rotate: y 180deg;
}

.card-front, .card-back {
  position: absolute;
  inset: 0;
  display: grid;
  place-content: center;
  border-radius: 50px;
  box-shadow: 0px 10px 15px rgba(0, 0, 0, 0.3);
  backface-visibility: hidden;
}

.card-front {
  background-color: #f6f7e8;
  border: 15px solid #7FCD91;
}

.card-back {
  background-color: #7FCD91;
  rotate: y 180deg;
}

.titles {
  font-size: 12vw;
  text-align: center;
  font-family: "asakim";
}

.text {
  font-size: 6vw;
  text-align: center;
  direction: rtl;
  font-family: "assistant";
  white-space: pre-wrap;
}

.slide-left-enter-active,
.slide-left-leave-active,
.slide-right-enter-active,
.slide-right-leave-active {
  transition: all 0.35s ease;
  position: absolute;
  width: 70vw;
  height: 40vh;
}

.slide-left-enter {
  transform: translateX(100%);
  opacity: 0;
}

.slide-left-enter-to {
  transform: translateX(0);
  opacity: 1;
}

.slide-left-leave-to {
  transform: translateX(-100%);
  opacity: 0;
}

.slide-right-enter {
  transform: translateX(-100%);
  opacity: 0;
}

.slide-right-enter-to {
  transform: translateX(0%);
  opacity: 1;
}

.slide-right-leave-to {
  transform: translateX(100%);
  opacity: 0;
}

.progress-wrapper {
  position: absolute;
  bottom: 10%;
  width: 80%;
  display: flex;
  flex-direction: column;
  align-items: center;
  transform: scaleX(-1);
}

.progress-label {
  font-size: 1.2em;
  margin-bottom: 0.5em;
  font-family: assistant;
}
.forwaedArrow{
    background-image: url("../assets/media/thinArrow.svg");
    width: 20vw;
    height: 20vh;
    background-repeat: no-repeat;
    position: absolute;
    top: 45%;
    left: -2%;
}
.forwaedArrow:active{
    background-image: url("../assets/media/activeForwardarrow.svg");
    transform: translateY(1px);
}
.backArrow{
    background-image: url("../assets/media/thinBackArrow.svg");
    width: 20vw;
    height: 20vh;
    background-repeat: no-repeat;
    position: absolute;
    top: 45%;
    left: 80%;
}
.backArrow:active{
    background-image: url("../assets/media/activeBackarrow.svg");
    transform: translateY(1px);
}

.toEndBtn{
        position: absolute;
        top: 90%;
        left: 5%;
        font-family: "asakim";
        color: #f6f7e8;
        text-shadow: 5px -2px 5px rgba(0, 0, 0, 0.5);
        background-color: #7FCD91;
        border-radius: 1.5vh;
        padding: 3%;
        width: 25vw;
        height: 3vh;
        font-size: 7vw;
        text-align: center;
        font-weight: 570;
        box-shadow: rgba(34, 34, 38, 0.2) 0px 7vw 29vw 0px;
}
</style>
