<template>
  <div>
    <canvas
      ref="game"
      width="640"
      height="480"
      style="border: 1px solid black;">
    </canvas>
  </div>
</template>

<script>
import io from 'socket.io-client'
export default {
  name: 'BlockGame',
  data () {
    return {
      socket: {},
      context: {},
      position: {
        x: 0,
        y: 0
      },
      p1y: 40,
      p2y: 40,
      pt: 10,
      ph: 100,
      bx: 50,
      by: 50,
      bd: 6,
      xv:  4,
      yv: 4,
      score2: 0,
      score1: 0,
      ais: 2,
    }
  },
  created () {
    this.socket = io('http://localhost:3000')
  },
  mounted () {
    this.context = this.$refs.game.getContext('2d')
    setInterval(update,1000/30)

    this.socket.on('position', data => {
      this.position = data
      this.context.clearRect(0, 0, this.$refs.game.width, this.$refs.game.height)
      this.context.fillStyle = '#FFFFFF'
      this.context.fillRect(0, 0, this.$refs.game.width, this.$refs.game.width)
      this.context.fillStyle = '#000000'
      this.context.fillRect(this.position.x, this.position.y, 20, 20)
    })
  },
  methods: {
    move (direction) {
      this.socket.emit('move', direction)
    },
    reset(){
      bx=c.width/2;
      by=c.height/2;
      xv=-xv;
      yv=3;
    },
    update(){
      this.bx+=this.xv;
      this.by+=this.yv;
      if(this.by<0 && this.yv<0){
          this.yv=-this.yv;
      }
      if(this.by>this.height&&this.yv<0){
          this.yv=-this.yv
      }
      if(this.by<0){
          if(this.by>this.p1y&&this.by<this.p1y+this.ph){
              this.xv=-this.xv;
              this.dy=this.by-(this.p1y+this.ph/2);
              this.yv = this.dy*0.3;

          }else{
              this.score2++;
              this.reset();
          }
      }
      if(this.by>this.width){
          if(this.by>this.p1y&&this.by<this.p2y+this.ph){
              this.xv=-this.xv;
              this.dy=this.by-(this.p2y+this.ph/2);
              this.yv = this.dy*0.3;

          }else{
              this.score1++;
              this.reset();
          }
      }
      if(this.p2y+this.ph/2<this.by){
          this.p2y+=this.ais;
      }else{
          this.p2y-=this.ais;
      }

      this.context.fillStyle='black'
      this.context.fillRect(0,0,c.width,c.height)
      this.context.fillStyle="white"
      this.context.fillRect(0,p1y,pt,ph)
      this.context.fillRect(c.width-pt,p2y,pt,ph)
      this.context.fillRect(bx-bd/2,by-bd/2,bd,bd)
      this.context.fillText(score1,100,100)
      this.context.fillText(score2,c.width-100,100)

    }

  }
}
</script>

<style scoped>

</style>
