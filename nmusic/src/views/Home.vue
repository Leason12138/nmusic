<template>
  <div class="home">
    <p class="sidetext">推荐歌单</p>
    <TuiJianItem
      class="tji"
      :item="item"
      v-for="item in tuijianlist.slice(0, 6)"
      :key="item.id"
    >
    </TuiJianItem>
    <p class="sidetext">最新音乐</p>
    <NewMusic
      :curMusic_id="curMusic_id"
      @clickfn="clickfn"
      class="newsong"
      :item="item"
      v-for="(item, index) in newsonglist"
      :idx="index"
      :key="item.id"
    >
    </NewMusic>
    <br />
    <br />
    <br />
  </div>

</template>
<script>
import TuiJianItem from "@/components/TuiJianItem.vue";
import NewMusic from "@/components/NewMusic.vue";

export default {
  components: { TuiJianItem, NewMusic },
  data: function () {
    return {
      tuijianlist: [],
      newsonglist: [],
      curMusic_id: "",
    };
  },
  methods: {
    clickfn(target, index) {
      // console.log(target);
      this.curMusic_id = target.id;
      this.$emit("changdiurl", target, index, this.newsonglist);
    },
  },
  mounted() {
    this.axios.get("personalized").then((res) => {
      this.tuijianlist = res.data.result;
    });
    this.axios.get("/personalized/newsong").then((res) => {
      // console.log(res);
      this.newsonglist = res.data.result;
      // console.log(res.data.result);
    });
  },
};
</script>
<style lang="scss" scoped>
.home {
  .sidetext {
    text-align: left;
    font-size: 16px;
    display: block;
    flex: 1 1 100vw;
    position: relative;
    margin-left: 15px;
  }
  .sidetext::before {
    content: "";
    display: block;
    position: absolute;
    left: -15px;
    width: 5px;
    height: 100%;
    background-color: #dd001b;
  }
  overflow: hidden;
  width: 100%;
  display: flex;
  justify-content: space-between;
  flex-wrap: wrap;
  padding: 0;
  margin: 0;
  .tji {
    width: 32vw;
    padding-bottom: 10px;
    margin: 0;
  }
  .tji:nth-child(3n + 2) {
    width: 32vw;
    padding: 0;
    margin: 0;
  }
  .newsong {
    display: block;
    width: 100%;
    height: 50px;
    text-align: left;
  }
}
</style>