<template>
  <div id="app">
    <div class="top">
      <div class="logo">
        <div class="img"></div>
        <div class="word"></div>
      </div>
      <div class="title">安防智能展区</div>
      <div class="top-nav">
        <div class='point' @click="changeActivePage('box1')" :class="activePage == 'box1' ?'selected':''"></div>
        <div class='point' @click="changeActivePage('box2')" :class="activePage == 'box2'?'selected':''"></div>
        <div class='point' @click="changeActivePage('box3')" :class="activePage == 'box3'?'selected':''"></div>
        <div class='point' @click="changeActivePage('box4')" :class="activePage == 'box4'?'selected':''"></div>
        <!-- <div class={this.state.to === 3? "point selected": "point"}></div> -->
      </div>
    </div>
    <div class="ele-img"></div>

    <router-view :activePage='activePage' @navChange='navChange'/>
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      box1: true,
      box2: false,
      box3: false,
      box4: false,
      activePage: "box1"
    };
  },
  methods: {
    navChange(box1, box2, box3, box4) {
      this.box1 = box1;
      this.box2 = box2;
      this.box3 = box3;
      this.box4 = box4;
    },
    changeActivePage(page) {
      // console.log(page);
      // this.activePage = page;
    }
  }
};
</script>

<style lang='scss'>
#app {
  // display: flex;
  // flex-direction: column;
  overflow: hidden;
  position: relative;
  height: 100%;
  color: #fff;
  background-image: url(./assets/bg_1920x1080.jpg);
  background-size: cover;
  background-position: center center;
  .top {
    width: 100%;
    background-image: url("./assets/Blue_Top.png");
    height: 75px;
    background-size: cover;
    background-repeat: no-repeat;
    display: flex;
    .logo {
      display: flex;
      .img {
        width: 82px;
        height: 77px;
        background-image: url(./assets/TSLlogo.png);
        background-size: 45px 45px;
        background-repeat: no-repeat;
        background-position: center center;
      }
      .word {
        height: 77px;
        width: 220px;
        background-image: url(./assets/terminus.png);
        background-size: 200px 25px;
        background-repeat: no-repeat;
        background-position: center center;
      }
    }
    .title {
      flex: 1;
      margin-left: 30px;
      line-height: 77px;
      font-size: 28px;
      font-weight: 700;
      letter-spacing: 22px;
    }
    .top-nav {
      width: 440px;
      height: 77px;
      display: flex;
      .point {
        width: 77px;
        height: 77px;
        background-image: url(./assets/file0.png);
        background-size: 60px 60px;
        background-repeat: no-repeat;
        background-position: center center;
        cursor: pointer;
        &.selected {
          background-image: url(./assets/file1.png);
        }
      }
    }
  }
  .ele-img {
    position: absolute;
    top: 75px;
    width: 100%; // background-image: url(./assets/Ele.png);
    height: 212px;
  }
}
</style>
