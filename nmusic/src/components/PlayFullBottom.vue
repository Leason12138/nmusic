<template>
  <div class="playfullbottom">
    <input
      class="ranger"
      type="range"
      min="0"
      :max="Songing.duration"
      @input="sentctimefn"
      :value="ctime"
    />
    <div class="btnLsit">
      <div class="btn playModel">⇢</div>
      <div class="btn prevSong" @click="$emit('prevSong')">◁</div>
      <div class="btn pauseSong" @click="$emit('changeStop')">
        <span v-if="runool" class="ctrl"> ▶ </span>
        <span v-else class="runing">■</span>
      </div>
      <div class="btn nextSong" @click="$emit('nextSong')">▷</div>
      <div class="btn songList">▥</div>
    </div>
  </div>
</template>

<script>
export default {
  props: ["Songing", "ctime", "runool"],
  data: function () {
    return {
      //   changeTime:"",
      // @input="$emit('changeTimeFn',)
    };
  },
  methods: {
    sentctimefn(e) {
      //   console.log(e.target.value);
      this.$emit("setctimefn", e.target.value);
    },
  },
};
</script>

<style lang="scss" scoped>
.playfullbottom {
  width: 100vw;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  background-color: #b62828;
  .ranger {
    width: 80vw;
  }
  .btnLsit {
    width: 80vw;
    height: 20vw;
    display: flex;
    flex-direction: row;
    justify-content: space-around;
    align-items: center;
    .btn {
      background-color: #fff;
      //playModel"
      // prevSong">
      // pauseSong"
      // nextSong">
      // songList">
      &.songList,
      &.playModel {
        width: 7.5vw;
        font-size: 3.75vw;
        height: 7.5vw;
        border-radius: 50%;
        line-height: 7.5vw;
        background-color: skyblue;
      }
      &.prevSong,
      &.nextSong {
        width: 8vw;
        height: 10vw;
        font-size: 6.66vw;
        padding-right: 1.6vw;
        border-radius: 50%;
        line-height: 10.3vw;
        background-color: skyblue;
      }
      &.nextSong {
        padding-right: 0;
        padding-left: 1.6vw;
      }
      &.pauseSong {
        width: 15vw;
        height: 15vw;
        font-size: 10vw;
        border-radius: 50%;
        line-height: 13.5vw;
        background-color: skyblue;
        //  ctrl">
       // runing"
        .ctrl {
          line-height: 15vw;
          font-size: 8vw;
          padding-left: 2vw;
        }
      }
    }
  }
}
</style>