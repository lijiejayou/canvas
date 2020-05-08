<template>
  <div>
    <canvas id="myCanvas">浏览器不支持</canvas>
  </div>
</template>

<script>
import ball from '@/utils/Ball.js'
export default {
  name: 'Home',
  data() {
    return {
      ballArray: [],
      ctx: '',
      canvasWidth: document.body.scrollWidth,
      canvasHeight: document.documentElement.clientHeight,
      colorArray: ['red', 'blue', 'green', 'purple', 'pink', 'yellow']
    }
  },
  mounted() {
    let myCanvasEle = document.getElementById('myCanvas')
    this.ctx = myCanvasEle.getContext('2d')
    myCanvasEle.height = this.canvasHeight
    myCanvasEle.width = this.canvasWidth
    myCanvasEle.style.background = 'black'

    //鼠标移动事件
    myCanvasEle.addEventListener('mousemove', e => {
      this.ballArray.push(ball.getBall(this.ctx, e.offsetX, e.offsetY, this.colorArray[Math.floor(Math.random() * this.colorArray.length)]))
    })

    //定时器
    setInterval(() => {
      this.clear()
      this.draw()
    }, 50)
  },
  methods: {
    clear() {
      //清屏
      this.ctx.clearRect(0, 0, this.canvasWidth, this.canvasHeight)
    },
    draw() {
      //绘制
      for (let i = 0; i < this.ballArray.length; i++) {
        this.ballArray[i].draw()
        this.ballArray[i].update()
      }
    }
  }
}
</script>

<style scoped>

</style>