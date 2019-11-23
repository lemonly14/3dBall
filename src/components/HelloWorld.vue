<!--  -->
<template>
  <transition name="moveL"
              enter-active-class="animated bounceInLeft"
              leave-active-class="animated bounceOutRight">
    <div v-if="show"
         class="rotating">
      <div class="top">
        <div>
          <img class="circle"
               src="http://imgsrc.baidu.com/forum/pic/item/e6b14bc2a4561b1fe4dd3b24.jpg "
               alt="">
        </div>
      </div>

      <div class="bottom">
        <p class="name">某某某</p>
        <p class="content">签到成功</p>
      </div>
    </div>
  </transition>
</template>

<script>
//这里可以导入其他文件（比如：组件，工具js，第三方插件js，json文件，图片文件等等）
//例如：import 《组件名称》 from '《组件路径》';

export default {
  //import引入的组件需要注入到对象中才能使用
  components: {},
  props: {
    show: {
      type: Boolean,
      default: false
    }
  },
  data() {
    //这里存放数据
    return {
      // show: true
    };
  },
  //监听属性 类似于data概念
  computed: {},
  //监控data中的数据变化
  watch: {
    show(newVal, oldVal) {
      // eslint-disable-next-line no-console
      console.log('newVal', newVal);
      // eslint-disable-next-line no-console
      console.log('oldVal', oldVal);
    }
  },
  //方法集合
  methods: {

  },
  //生命周期 - 创建完成（可以访问当前this实例）
  created() {

  },
  //生命周期 - 挂载完成（可以访问DOM元素）
  mounted() {

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
/* //@import url(); 引入公共css类 */
.rotating {
  width: 17.5vw;
  height: 22vw;
  display: inline-flex;
  margin: auto;
  position: fixed;
  top: 25%;
  left: 44%;
  z-index: 1;
  opacity: 0.9;
  border-radius: 45px;
  background: linear-gradient(to right, #7579b9, #37a2dc, #76c7cd, #9fd0ea);
  display: flex;
  flex-direction: column;
  .top {
    width: 100%;
    height: 70%;
    /* background: #ce1313; */
    border-radius: 45px;
    position: relative;
    .circle {
      width: 12vw;
      height: 12vw;
      border-radius: 50%;
      background: #ffffff;
      position: absolute;
      margin: auto;
      top: 0;
      left: 0;
      bottom: 0;
      right: 0;
    }
  }
  .bottom {
    width: 100%;
    height: 30%;
    border-radius: 45px;
    position: relative;
    /* background: #0096ff; */
    /* display: flex; */
    /* justify-content: center;
    align-items: center; */
    .name {
      width: 100%;
      text-align: center;
      color: #ffffff;
      font-size: xxx-large;
      font-weight: 100;
      position: absolute;
      top: -45%;
    }
    .content {
      width: 100%;
      text-align: center;
      color: #ffffff;
      font-size: 35px;
      font-weight: 800;
      position: absolute;
      top: 18%;
    }
  }
}
</style>
