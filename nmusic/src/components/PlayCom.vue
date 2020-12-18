<template>
  <div class="play">
    <audio
      class="mplayer"
      :src="
        'https://music.163.com/song/media/outer/url?id=' + mp3datail.id + '.mp3'
      "
      autoplay
      ref="audio"
    ></audio>
    <transition
      name="custom-classes-transition"
      enter-active-class="animate__animated animate__slideInUp animate__slow	"
      leave-active-class="animate__animated animate__slideOutDown animate__faster "
    >
      <div v-show="isbarshow&&mp3datail.name "  class="palybar">
        <div class="musicshow" @click="isbarshow = !isbarshow">
          <div class="pic" ref="pic">
            <div
              class="picinside"
              :style="{ background: 'url(' + mp3datail.picUrl + ') ' }"
            ></div>
          </div>
          <span  v-if="mp3datail.song" class="musicname"
            >{{ mp3datail.name }} - {{mp3datail.song.album.name }}</span
          >
        </div>
        <div class="mplayer-control">
          <!-- <canvas id="canvas"></canvas> -->

          <span @click="changeStop" v-if="runool" class="ctrl"> ▶ </span>
          <span @click="changeStop" v-else class="runing">■</span>
        </div>
      </div>
    </transition>
    <transition
      name="custom-classes-transition"
      enter-active-class="animate__animated animate__slideInUp animate__faster	"
      leave-active-class="animate__animated animate__slideOutDown animate__fast"
    >
      <div v-show="!isbarshow" class="palyfull">
        <PlayFullTop
          class="PlayFullTop"
          @resIsBarShow="isbarshow = !isbarshow"
        />
        <PlayFullView
        :runool='runool'
          :mp3datail="mp3datail"
          class="midle-box PlayFullView"
          @ViewOrLyric="midleShow = !midleShow"
          v-show="midleShow"
        />
        <PlayFullLyric
          class="midle-box PlayFullLyric"
          @ViewOrLyric="midleShow = !midleShow"
          v-show="!midleShow"
        />
        <PlayFullBottom
          class="PlayFullBottom"
          :Songing="Songing"
          :ctime="ctime"
          :runool="runool"
          @changeTimeFn="changeTimeFn"
          @setctimefn="setctimefn"
          @nextSong="nextSong"
          @prevSong="prevSong"
          @changeStop="changeStop"
        />
      </div>
    </transition>
  </div>
  <!-- <div v-if="isShowBar"></div>
<div v-if="!isShowBar"></div> -->
</template>

<script>
import PlayFullView from "@/components/PlayFullView";
import PlayFullLyric from "@/components/PlayFullLyric";
import PlayFullTop from "@/components/PlayFullTop";
import PlayFullBottom from "@/components/PlayFullBottom";
export default {
  components: {
    PlayFullView,
    PlayFullLyric,
    PlayFullTop,
    PlayFullBottom,
  },
  props: ["songlist", "index"],
  data: function () {
    return {
      runool: false,
      isbarshow: true,
      Songing: "",
      ctime: "",
      mp3datail: {},
      canClacIndex: "",
      midleShow: true,
    };
  },
  methods: {
    setctimefn(time) {
      let audio = this.$refs.audio;
      let pic = this.$refs.pic;
      audio.currentTime = time;
      this.runSong(audio, pic);
    },
    changeTimeFn(tt) {
      tt;
      // console.log(tt);
    },
    changeStop() {
      let audio = this.$refs.audio;
      let pic = this.$refs.pic;
      if (this.runool) {
        this.runSong(audio, pic);
      } else {
        this.stopSong(audio, pic);
      }
    },
    stopSong(audio, pic) {
      audio.pause();
      pic.classList.add("picstop");
      console.log('iampicstop');
      this.runool = audio.paused;
    },
    runSong(audio, pic) {
      audio.play();
      this.runool = audio.paused;
      pic.classList.remove("picstop");
    },
    nextSong() {
      this.canClacIndex++;
    },
    prevSong() {
      this.canClacIndex--;
    },
  },
  updated() {
    let that = this;
    let pic = this.$refs.pic;
    let audio = this.$refs.audio;
    audio.ontimeupdate = function () {
      that.Songing = this;
      that.ctime = this.currentTime;
      if (this.ended) {
        that.stopSong(this, pic);
      }
    };
  },
  watch: {
    mp3datail: function () {
      let audio = this.$refs.audio;
      let pic = this.$refs.pic;
      this.runSong(audio, pic);
    },
    index: function (n) {
      this.canClacIndex = n;
    },
    canClacIndex: function (n) {
      this.mp3datail = this.songlist[n];
    },
  },
};
</script>

<style lang="scss" scoped>
.play {
  z-index: 10;
  // display: flex;
  // justify-content: space-between;
  // align-items: center;
  position: relative;
  // background-color: #c2c2c2;
  .palybar {
    width: 100vw;
    background-color: darkgrey;
    height: 8vh;
    position: absolute;
    bottom: 0;
    .musicshow {
      position: absolute;
      left: 0;
      top: 42%;
      width: 68vw;
      // background-color: pink;
      transform: translateY(-50%);
      display: flex;
      justify-content: space-between;
      align-items: center;
      .pic {
        margin: 0 0 7px 7px;
        width: 13.5vw;
        height: 13.5vw;
        background: url("../assets/black_pad.png") no-repeat;
        background-size: contain;
        border-radius: 50%;
        animation: picTurnRound 3.5s linear infinite;
        display: flex;
        justify-content: center;
        align-items: center;
        .picinside {
          width: 8.2vw;
          height: 8.2vw;
          border-radius: 50%;
        }
      }
      .picstop {
      animation-play-state: paused;
      -webkit-animation-play-state: paused; 
    }
      .musicname {
        text-align: center;
        height: 8vw;
        font-size: 14px;
        line-height: 8vw;
        white-space: nowrap;
        width: 48vw;
        color: #fafafa;
        display: -webkit-box;
        -webkit-box-orient: vertical;
        -webkit-line-clamp: 2;
        overflow: hidden;
        text-overflow: ellipsis;
        background-color: transparent;
      }
    }
    // .mplayer {
    //   width: 50vw;
    //   background-color: red;
    // }
    .mplayer-control {
      width: 28vw;
      line-height: 40px;
      position: absolute;
      right: -3vw;
      top: 42%;
      transform: translateY(-50%);

      .runing {
        display: inline-block;
        width: 20px;
        height: 20px;
        line-height: 17px;
        text-align: center;
        font-size: 20px;
        color: #fafafa;
        border: 2px solid #fafafa;
        border-radius: 50%;
      }
      .ctrl {
        display: inline-block;
        width: 17px;
        height: 20px;
        padding-left: 3px;
        line-height: 23px;
        text-align: center;
        font-size: 12.5px;
        color: #fafafa;
        border: 2px solid #fafafa;
        border-radius: 50%;
      }
    }
  }
  .palyfull {
    z-index: 100;
    width: 100vw;
    height: 100vh;
    background-color: #ddd;
    display: block;
    position: relative;
    .PlayFullBottom {
      position: absolute;
      bottom: 0;
    }
  }
}
@keyframes picTurnRound {
  from {
    transform: rotate(0);
  }
  to {
    transform: rotate(360deg);
  }
}
</style>