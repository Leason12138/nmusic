<template>
  <div @click="$emit('ViewOrLyric')">
    PlayFullView
    <div class="pic" ref="pic">
      <div
        class="picinsilde"
        :style="{ background: 'url(' + mp3datail.picUrl + ') ' }"
      ></div>
    </div>
    <div>
      <span>{{ mp3datail.name }}</span>
    </div>
  </div>
</template>

<script>
export default {
  props: ["mp3datail", "runool"],
  mounted() {
    // console.log(this.mp3datail.picUrl);
  },
  watch: {
    runool: function (n) {
      // console.log(n);
      if (n) {
        this.$refs.pic.classList.add("picstop");
      }else{
        this.$refs.pic.classList.remove("picstop");
      }
    },
  },
};
</script>

<style lang="scss" scoped>
.PlayFullView {
  background-color: #cccccc;
  width: 100vw;
  height: 75vh;
  display: flex;
  flex-direction: column;
  justify-content: space-around;
  align-items: center;
  .pic {
    background: url("../assets/black_pad.png") no-repeat;
    animation: picTurnRound 3.5s linear infinite;
    background-size: contain;
    width: 76vw;
    height: 76vw;
    display: flex;
    justify-content: center;
    align-items: center;
    .picinsilde {
      z-index: 6;
      background-repeat: no-repeat;
      background-size: cover;
      width: 52.5vw;
      height: 52.5vw;
      border-radius: 50%;
      background-color: transparent;
    }
  
  }
    .picstop {
      animation-play-state: paused;
      -webkit-animation-play-state: paused; 
    }
  @keyframes picTurnRound {
    from {
      transform: rotate(0);
    }
    to {
      transform: rotate(360deg);
    }
  }
}
</style>