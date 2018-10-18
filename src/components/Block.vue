<template>
<div class="block">
    <div class="block-top">
        <div class='block-title'>
            <span>{{index}}</span>
            <span>安防智能展区</span>
        </div>
    </div>
    <div class="block-body" :class="position">
        <div class="video" :id='id'>

        </div>
        <div class="list">
          <transition-group name="list" tag="div">
            <div class="line" v-for="item in list" :key="item.id">
                <div class="avator">
                  <img :src="`data:image/gif;base64,${item.image}`" alt="">
                </div>
                <div class="age">
                    <span class="key">age</span>
                    <span class="value">{{item.age}}</span>
                </div>
                <div class="sex" :class="item.sex == 1? 'man':'woman'" ></div>
                <div class="mood"  :class="item.emotion == 1? 'smile':'confused'" ></div>
            </div>
          </transition-group>
            
        </div>
    </div>
</div>
</template>
<script>
export default {
  data() {
    return {
      client: null,
      list: []
    };
  },
  props: ["position", "id", "index", "url", "subscribe"],
  created() {
    // setInterval(() => {
    //   if (this.list.length > 5) {
    //     this.list = this.list.splice(0, 4);
    //   }
    //   this.list.unshift({
    //     key: new Date()
    //   });
    // }, 3000);
  },
  mounted() {
    // console.log(this.$mqtt);
    this.initVideo();

    this.client = this.$mqtt.connect("ws://192.168.100.141:9001");
    let _this = this;
    this.client.on("connect", () => {
      _this.client.subscribe(this.subscribe, err => {
        if (!err) {
          // _this.client.publish('test','hello')
        }
      });
    });
    this.client.on("message", (topic, message) => {
      // console.log("topic", topic);
      // console.log(JSON.parse(message), "response");
      // _this.client.end()
      if (_this.list.length > 15) {
        _this.list = _this.list.splice(0, 4);
      }
      _this.list.unshift(JSON.parse(message));
    });
  },
  methods: {
    initVideo() {
      var player = new Aliplayer(
        {
          id: this.id,
          source: this.url,
          width: "422px",
          height: "240px",
          autoplay: true,
          isLive: false,
          rePlay: false,
          showBuffer: true,
          snapshot: false,
          showBarTime: 5000,
          useFlashPrism: true,
          skinLayout: [
            {
              name: "controlBar",
              align: "blabs",
              x: 0,
              y: 0,
              children: [
                {
                  name: "playButton",
                  align: "tl",
                  x: 15,
                  y: 26
                }
              ]
            },
            {
              name: "fullControlBar",
              align: "tlabs",
              x: 0,
              y: 0,
              children: []
            }
          ]
        },
        function(player) {
          console.log("播放器创建了。");
        }
      );
    }
  },
  watch: {
    url() {
      //   console.log("url变化了");
      //   this.initVideo();
    }
  }
};
</script>
<style lang="scss">
.block {
  .block-top {
    height: 99px;
    width: 100%;
    background-position: center center;
    background-repeat: no-repeat;
    position: relative;
    background-image: url(./../assets/Title.png);
    .block-title {
      position: absolute;
      left: 50%;
      transform: translateX(-100%);
      color: #fff;
      width: 230px;
      line-height: 97px;
      font-size: 26px;
      font-weight: 700;
    }
  }
  .block-body {
    position: relative;
    height: 1438px;
    width: 100%;
    background-position: center center;
    background-repeat: no-repeat;
    padding-top: 40px;
    &.left {
      background-image: url(./../assets/Blue_Left.png);
    }
    &.mid {
      background-image: url(./../assets/Blue_Mid.png);
    }
    &.right {
      background-image: url(./../assets/Blue_Right.png);
    }
    .video {
      position: absolute;
      left: 50%;
      transform: translateX(-51%);
      width: 440px !important;
      height: 320px;
      background-image: url(./../assets/Video_frame.png);
      background-position: center center;
      background-repeat: no-repeat;
      background-size: 492px 320px;
      padding-top: 36px;
      position: relative;
      .prism-ErrorMessage {
        display: none !important;
      }
      video {
        // background-color: yellowgreen;
        width: 440px !important;
        height: 250px;
        position: absolute;
        top: 0px;
        left: 50%;
        transform: translateX(-51%);
      }
    }
    .list {
      padding-top: 10px;
      height: 366px;
      overflow: hidden;

      .list-enter-active,
      .list-leave-active {
        transition: all 3s;
      }
      .list-enter,
      .list-leave-to {
        opacity: 0;
        // transform: translateX(100px);
      }
      .line {
        height: 122px;
        background-image: url(./../assets/Info_frame.png);
        background-repeat: no-repeat;
        background-position: center center;
        display: flex;
        position: relative;
        transition: all 1s;
        .avator {
          position: absolute;
          left: 50%;
          top: 20px;
          transform: translateX(-260%);
          width: 85px;
          height: 85px;
          background-image: url(./../assets/Face_frame.png);
          img {
            width: 85px;
            height: 85px;
          }
        }
        .age {
          color: #fff;
          font-weight: 400;
          position: absolute;
          left: 50%;
          top: 20px;
          transform: translateX(-126%);
          height: 85px;
          .key {
            font-size: 26px;
            font-family: Impact, Charcoal, sans-serif;
          }
          .value {
            font-size: 28px;
            line-height: 85px;
            margin-left: 16px;
            font-family: "Comic Sans MS", cursive, sans-serif;
          }
        }
        .sex {
          position: absolute;
          left: 50%;
          top: 20px;
          transform: translateX(10%);
          height: 85px;
          width: 85px;
          background-size: 60px 60px;
          background-position: center center;

          &.man {
            background-image: url(./../assets/man.png);
          }
          &.woman {
            background-image: url(./../assets/Woman.png);
          }
        }
        .mood {
          position: absolute;
          left: 50%;
          top: 20px;
          transform: translateX(116%);
          height: 85px;
          width: 85px;
          background-size: 60px 60px;
          background-position: center center;
          &.smile {
            background-image: url(./../assets/smile.png);
          }
          &.confused {
            background-image: url(./../assets/confused.png);
          }
        }
      }
    }
  }
}
</style>
