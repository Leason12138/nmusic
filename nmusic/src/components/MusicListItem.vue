<template>
  <div class="Hotitems" @click="$emit('clickfn', item,idx)">
    <div class="left">
      <span>
        <span class="text">
          {{ item.name }}
        </span>
        <span v-if="item.al.name" class="chinese">
          {{ item.al.name }}
        </span>
      </span>
      <br />
      <span class="auther" v-for="it in item.ar" :key="it.id">
        {{ it.name }}
      </span>
      <p class="zhuangji">-{{ item.al.name }}</p>
    </div>
    <div class="right">
      <span v-if="curMusic_id==item.id" class="runing">■</span>
      <span v-else class="ctrl"> ▶ </span>
    </div>
  </div>
</template>

<script>
export default {
  props: ["item", "curMusic_id",'idx'],
  methods: {},
  data: function () {
    return {
    };
  },
  created() {},
};
</script>

<style lang="scss" scoped>
.Hotitems {
  width: 100vw;
  padding-top: 5px;
  margin-left: 10px;
  height: 55px;
  border-bottom: 1px #eee solid;
  .left {
    float: left;
    width: 60vw;
    .text {
      font-size: 17px;
      white-space: nowrap;
    }
    .chinese {
      font-size: 17px;

      color: #999;
      &::before {
        content: "(";
      }
      &::after {
        content: ")";
      }
    }
    .auther {
      font-size: 10px;
      color: #888;
      &:last-of-type {
        &::after {
          content: "";
        }
      }
      &::after {
        content: "/";
      }
    }
    .zhuangji {
      display: inline;
      font-size: 10px;
      color: #888;
    }
  }
  .right {
    float: right;
    width: 12vw;
    margin: 1px 5px 0px 0px;
    height: 41px;
    display: flex;
    justify-content: center;
    align-items: center;
    .runing{
       width: 20px;
      height: 20px;
      line-height: 17px;
      font-size: 20px;
      text-align: center;
      color: #dd001b;
      border: 2px solid #dd001b;
      border-radius: 50%;
    }
    .ctrl {
      width: 20px;
      height: 20px;
      line-height: 20px;
      text-align: center;
      font-size: 12px;
      color: #aaa;
      border: 2px solid #aaa;
      border-radius: 50%;
    }
  }
}
</style>