<template>
  <button id="button" @click="startPlaying">play</button>
  <p v-show="stopPlaying">Reaction Result: {{reactionResult}}</p>
  <div class="boxContainer" ref="container" v-show="containerShowing">
    <div class="box" ref="box" v-show="isPlaying" @click="stopTimer()"></div>
  </div>
</template>

<script>

export default {
  name: 'App',
  data() {
    return{
      containerShowing: false,
      isPlaying: false,
      delay: null,
      timer: null,
      reaction: 0,
      reactionResult: '',
      stopPlaying: false
    }
  },
  methods: {
    startPlaying() {
      document.getElementById("button").disabled = true
      this.containerShowing = true
      this.stopPlaying = false
      this.delay= 2000 + Math.random() * 3000
      // container size:
      let containerSize = 200 + Math.random() * 400
      this.$refs.container.style.height = `${containerSize}px`
      // box size:
      let boxSize = 50 + Math.random() * 100
      this.$refs.box.style.height = `${boxSize}px`
      this.$refs.box.style.width = `${boxSize}px`
      // box position:
      let position= 1 + Math.random() * (containerSize - boxSize)
      this.$refs.box.style.top = `${position}px`
      this.$refs.box.style.left = `${position}px`
      setTimeout(()=> {
        this.isPlaying= true
        this.startTimer()
      }, this.delay)
    },
    startTimer() {
      this.timer = setInterval(()=> {
        this.reaction += 10
      },10)
    },
    stopTimer() {
      document.getElementById("button").disabled = false
      this.isPlaying = false
      this.stopPlaying = true
      this.containerShowing = false
      clearInterval(this.timer)
      console.log(this.reaction);
      if(this.reaction < 1000){
        this.reactionResult = 'Good'
      }
      else if(this.reaction > 1000 && this.reaction < 2000) {
        this.reactionResult = 'Not Bad'
      }else {
        this.reactionResult = 'Bad'
      }
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 30px;
}
button {
  height: 40px;
  width: 60px;
  font-size: 15px;
  border-color: transparent;
  border-radius: 5px;
  cursor: pointer;
}
.boxContainer {
  border: 1px solid black;
  margin-top: 20px;
  width: 100%;
  position: relative;
}
.box {
  background-color: black;
  position: absolute;
  cursor: pointer;
}
</style>
