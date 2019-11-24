<!--  -->
<template>
  <div class='ground'>
    <div id="container"
         class="container"></div>
    <HelloWorld :show="show" />
    <button @click="change()">
      Toggle render
    </button>
    <div class="container1">
      <div class="message">
        <marquee align="middle"
                 scrollamount="10">{{ scrollText }}</marquee>
      </div>
      <div class="message3">
        <div class="pcontainer"
             v-for="(item,index) in 9"
             :key="index">
          <div class="pic">
            <img src="http://imgsrc.baidu.com/forum/pic/item/e6b14bc2a4561b1fe4dd3b24.jpg"
                 class="face-img">
            <span class="fontstyle">某某某</span>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
//这里可以导入其他文件（比如：组件，工具js，第三方插件js，json文件，图片文件等等）
//例如：import 《组件名称》 from '《组件路径》';
import raf from 'raf'
// import { Transform } from '../public/static/transform'
import HelloWorld from './components/HelloWorld'

export default {
  //import引入的组件需要注入到对象中才能使用
  components: {
    HelloWorld
  },
  data() {
    //这里存放数据
    return {
      clientWidth: document.body.clientWidth,
      img_list: [],
      center: { x: 200, y: 900, z: 100 },
      camera_position: { x: 0, y: 300, z: 500 },
      r: 350,
      // r: 500,
      distance: 300,
      // distance: 600,
      positions: [],
      rd_positions: [],
      step_angle: Math.PI / 180,
      size: 400,
      img_Arr: [],
      show: false,
      scrollText: '欢迎领导莅临星网锐捷展厅参观'
    };
  },
  //监听属性 类似于data概念
  computed: {},
  //监控data中的数据变化
  watch: {
    clientWidth(newWidth) {
      // eslint-disable-next-line no-console
      console.log('newWidth', newWidth);
    }
  },
  //方法集合
  methods: {
    change() {
      this.show = !this.show
    },
    getRandomNumber(min, max) {
      return min + Math.floor(Math.random() * (max - min + 1));
    },
    randomPoints() {
      let j = -1
      for (let i = 0; i < this.size; i++) {
        let x = this.getRandomNumber(-350, 350)
        let y = this.getRandomNumber(-350, 350)
        j = j * -1
        if (x * x + y * y <= this.r * this.r) {
          let z = j * Math.sqrt(Math.abs(this.r * this.r - x * x - y * y));
          this.positions.push({ x: x, y: y, z: z });
          this.rd_positions.push({ x: x, y: y, z: z });
        }
      }
    },
    rotate() {
      for (let i = 0; i < this.positions.length; i++) {
        let cx = this.positions[i].x
        // eslint-disable-next-line no-unused-vars
        let z = this.positions[i].z
        this.positions[i].x = cx * Math.cos(this.step_angle) - z * Math.sin(this.step_angle);
        this.positions[i].z = z * Math.cos(this.step_angle) + cx * Math.sin(this.step_angle);
      }
    },
    createImgs() {
      for (let i = 0; i < this.positions.length; i++) {
        let img = document.createElement("img")
        // img.style.position = "absolute";
        // img.style.left = "0px";
        // img.style.top = "0px";
        // img.style.height = "100px";
        // img.style.width = "100px";
        img.style.cssText = 'position:absolute;left:50px;top:50px;height:100px;width:100px;'
        img.src = "http://imgsrc.baidu.com/forum/pic/item/e6b14bc2a4561b1fe4dd3b24.jpg";
        document.getElementById("container").appendChild(img);
        // eslint-disable-next-line no-undef
        Transform(img, true);
        this.transformImg(img, i);
        this.img_list.push(img);
      }
    },
    transformImg(img, i) {
      let z = this.positions[i].z
      img.translateX = this.center.x + this.rd_positions[i].x;
      img.translateY = this.center.x + this.rd_positions[i].y;
      //projection
      img.scaleX = img.scaleY = 0.5 * this.distance / Math.abs(this.camera_position.z - z);
      img.style.opacity = 0.1 + 1 - (this.r - z) / (2 * this.r);
    },
    render() {
      for (let i = 0; i < this.positions.length; i++) {
        this.transformImg(this.img_list[i], i);
      }
    },
    positionsProjection() {
      for (let i = 0; i < this.positions.length; i++) {
        let p = this.positions[i]
        let rp = this.rd_positions[i]
        rp.x = p.x;
        rp.y = p.y;
      }
    },
    tick() {
      this.rotate();
      this.positionsProjection();
      this.render();
      raf(this.tick.bind(this))
    },
  },
  //生命周期 - 创建完成（可以访问当前this实例）
  created() {
  },
  //生命周期 - 挂载完成（可以访问DOM元素）
  mounted() {
    this.randomPoints()
    this.createImgs()
    this.positionsProjection()
    raf(this.tick.bind(this))

  },
  beforeCreate() { }, //生命周期 - 创建之前
  beforeMount() { }, //生命周期 - 挂载之前
  beforeUpdate() { }, //生命周期 - 更新之前
  updated() { }, //生命周期 - 更新之后
  beforeDestroy() { }, //生命周期 - 销毁之前
  destroyed() { }, //生命周期 - 销毁完成
  activated() { }, //如果页面有keep-alive缓存功能，这个函数会触发
}

</script>
<style lang="scss" scoped>
@import url("../public/static/animate.css");
.ground {
  width: 100%;
  height: 100%;
  position: absolute;
  background: #000000;
  margin: 0;
  background-image: url("./assets/go.gif");
  background-size: 100% 100%;
  .container {
    width: 600px;
    height: 600px;
    position: absolute;
    /* background: #000000; */
    margin: auto;
    top: 0;
    left: -50%;
    bottom: 0;
    right: 0;
  }
  .container1 {
    width: 45%;
    height: 100%;
    position: absolute;
    /* background: #000000; */
    margin: auto;
    top: 0;
    left: 0;
    bottom: 0;
    right: -40%;
    display: flex;
    flex-direction: column;
    .message {
      width: 100%;
      height: 18%;
      /* background: #123445; */
      padding: 5% 17%;
      background-image: url("./assets/frame.png");
      background-size: cover;
      margin-top: 8%;
      font-size: -webkit-xxx-large;
      color: #ffffff;
    }
    .message3 {
      width: 100%;
      height: 73%;
      /* background: #12aa45; */
      display: flex;
      flex-flow: wrap;
      justify-content: space-evenly;
      .pcontainer {
        width: 30%;
        height: 33%;
        /* background: #92a145; */
        display: flex;
        flex-direction: row;
        justify-content: center;
        align-items: center;
        .pic {
          width: 9vw;
          height: 9vw;
          border-radius: 50%;
          position: relative;
          display: flex;
          flex-direction: column;
          justify-content: center;
          align-items: center;
          background: linear-gradient(
            to right,
            #7579b9,
            #37a2dc,
            #76c7cd,
            #9fd0ea
          );
          .face-img {
            width: 7.5vw;
            height: 7.5vw;
            position: absolute;
            margin: auto;
            top: 0;
            left: 0;
            bottom: 0;
            right: 0;
            border-radius: 50%;
          }
          .fontstyle {
            margin-top: 10.5vw;
            color: #ffffff;
            font-size: large;
          }
        }
      }
    }
  }
}
</style>
