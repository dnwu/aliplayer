<template>
    <div class="page">
        <transition 
            name="fade"
            v-on:before-enter="fade1beforeEnter"
            v-on:enter="fade1enter"
            v-on:after-enter="fade1afterEnter"


            v-on:before-leave="fade1beforeLeave"
            v-on:leave="fade1leave"
            v-on:after-leave="fade1afterLeave"
        >
            <div class="box box1" ref="box1" v-show="activePage=='box1'?true:false">
                <div class="left">
                    <Block :subscribe="'/ATT/CH01/'" :url="streamUrl[0]" index='1' position='left' id="box1-left"></Block>
                </div>
                <div class="mid">
                    <Block :subscribe="'/ATT/CH02/'" :url="streamUrl[1]" index='2' position='mid' id="box1-mid"></Block>
                </div>
                <div class="right">
                    <Block :subscribe="'/ATT/CH03/'" :url="streamUrl[2]" index='3' position='right' id="box1-right"></Block>
                </div>
            </div>
        </transition>

        <transition
            name="fade"
            v-on:before-enter="fade1beforeEnter"
            v-on:enter="fade1enter"
            v-on:after-enter="fade1afterEnter"


            v-on:before-leave="fade1beforeLeave"
            v-on:leave="fade1leave"
            v-on:after-leave="fade1afterLeave"
         >
            <div class="box box2" ref="box2" v-show="activePage=='box2'?true:false">
                <div class="left">
                    <Block :url="streamUrl[3]" index='4' position='left' id="box2-left"></Block>
                </div>
                <div class="mid">
                    <Block :url="streamUrl[4]" index='5' position='mid' id="box2-mid"></Block>
                </div>
                <div class="right">
                    <Block :url="streamUrl[5]" index='6' position='right' id="box2-right"></Block>
                </div>
            </div>
        </transition>

        <transition
            name="fade"
            v-on:before-enter="fade1beforeEnter"
            v-on:enter="fade1enter"
            v-on:after-enter="fade1afterEnter"


            v-on:before-leave="fade1beforeLeave"
            v-on:leave="fade1leave"
            v-on:after-leave="fade1afterLeave"
        >
            <div class="box box3" ref="box3" v-show="activePage=='box3'?true:false">
                <div class="left">
                    <Block :url="streamUrl[6]" index='7' position='left' id="box3-left"></Block>
                </div>
                <div class="mid">
                    <Block :url="streamUrl[7]" index='8' position='mid' id="box3-mid"></Block>
                </div>
                <div class="right">
                    <Block :url="streamUrl[8]" index='9' position='right' id="box3-right"></Block>
                </div>
            </div>
        </transition>


        <transition
            name="fade"
            v-on:before-enter="fade1beforeEnter"
            v-on:enter="fade1enter"
            v-on:after-enter="fade1afterEnter"


            v-on:before-leave="fade1beforeLeave"
            v-on:leave="fade1leave"
            v-on:after-leave="fade1afterLeave"
        >
            <div class="box box4" ref="box4" v-show="activePage=='box4'?true:false">
                <div class="left">
                    <Block :url="streamUrl[9]" index='10' position='left' id="box4-left"></Block>
                </div>
                <div class="mid">
                    <Block :url="streamUrl[10]" index='11' position='mid' id="box4-mid"></Block>
                </div>
                <div class="right">
                    <Block :url="streamUrl[11]" index='12' position='right' id="box4-right"></Block> 
                </div>
            </div>
        </transition>
    </div>
</template>
<script>
import Block from "./Block";
export default {
  components: { Block },
  props: ["activePage"],
  data() {
    return {
      box1: true,
      box2: false,
      box3: false,
      box4: false,
      boxDOM: ["box1", "box2", "box3", "box4"],
      streamUrl: [
        "http://192.168.100.141:8080/live?port=1985&app=test&stream=stream1",
        "http://192.168.100.141:8080/live?port=1985&app=test&stream=stream1",
        "http://192.168.100.141:8080/live?port=1985&app=test&stream=stream1",
        "http://192.168.100.141:8080/live?port=1985&app=test&stream=stream1",
        "http://192.168.100.141:8080/live?port=1985&app=test&stream=stream1",
        "http://192.168.100.141:8080/live?port=1985&app=test&stream=stream1",
        "http://192.168.100.141:8080/live?port=1985&app=test&stream=stream1",
        "http://192.168.100.141:8080/live?port=1985&app=test&stream=stream1",
        "http://192.168.100.141:8080/live?port=1985&app=test&stream=stream1",
        "http://192.168.100.141:8080/live?port=1985&app=test&stream=stream1",
        "http://192.168.100.141:8080/live?port=1985&app=test&stream=stream1",
        "http://192.168.100.141:8080/live?port=1985&app=test&stream=stream1"
      ],
      titleArr: [
        "达尔文平台展区",
        "智能社区解决方案展区",
        "智能商业解决方案展区",
        "智能硬件展区",
        "室内定位系统展区",
        "智能医院解决方案展区",
        "智能校园解决方案展区",
        "智能写字楼展区",
        "智能警务解决方案展区",
        "智能安防解决方案展区",
        "展厅入口",
        "前台接待区"
      ]
    };
  },
  mounted() {
    this.initDOM();
    clearInterval(this.timer);
    let index = 0;
    // this.timer = setInterval(() => {
    //   if (index > 3) {
    //     index = 0;
    //   }
    //   let show, hide;
    //   if (index === 0) {
    //     show = this.boxDOM[1];
    //     hide = this.boxDOM[0];
    //   } else if (index === 3) {
    //     show = this.boxDOM[0];
    //     hide = this.boxDOM[3];
    //   } else {
    //     show = this.boxDOM[index + 1];
    //     hide = this.boxDOM[index];
    //   }
    //   this[show] = true;
    //   this[hide] = false;
    //   index++;
    //   this.navChange()
    // }, 30000);

    // setTimeout(() => {
    //   this.box1 = true;
    // }, 4000);
  },
  methods: {
    initDOM() {
      //   this.$refs.box1.style.left = "100vw";
    },
    navChange() {
      this.$emit("navChange", this.box1, this.box2, this.box3, this.box4);
    },
    toleft() {},
    toright() {},
    fade1beforeEnter(el) {
      //   console.log(el);
      //   console.log("fade1beforeEnter");
      //   el.style.left = "0vw";
    },
    fade1enter(el, done) {
      // console.log(el);
      //   el.style.left = "0vw";
      el.addEventListener("transitionend", done);
    },
    fade1afterEnter(el) {
      // el.style.left = "100vw";
    },
    fade1beforeLeave(el) {
      //   console.log("fade1beforeLeave");
      //   el.style.left = "0";
    },
    fade1leave(el, done) {
      //   el.style.left = "-100vw";
      el.addEventListener("transitionend", done);
    },
    fade1afterLeave(el) {
      //   console.log("fade1afterLeave");
      //   el.style.left = "100vw";
    }
  }
};
</script>
<style lang="scss" scoped>
.page {
  height: 1600px;
  position: relative;
  .box {
    // position: absolute;
    // transition: left 1s linear;
    width: 100%;
    height: 100%;
    display: flex;
    > div {
      flex: 1;
    }
  }
  .fade-enter {
    left: 100vw;
    opacity: 0;
  }
  .fade-leave-to {
    left: -100vw;
    opacity: 0;
  }
  .fade-enter-to,
  .fade-leave {
    left: 0vw;
    opacity: 1;
  }
  .fade-enter-active {
    transition: all 400ms linear;
  }
  .fade-leave-active {
    transition: all 400ms linear;
  }
}
</style>
