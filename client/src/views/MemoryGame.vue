<template>
  <div class="hash">
    <div v-for="(box, x) in game" :key="x">
      <div v-for="(b, y) in box" :key="y" class="box" @click="mark(x,y)">
        <span>{{b}}</span>
      </div>
    </div>
  </div>
</template>

<script>
import io from 'socket.io-client'
export default {
  name: 'BlockGame',
  data(){
    return {
      socket: {},
      context: {},
      position: {
        x: 0,
        y: 0
      },
      game: [
        ['', '', ''],
        ['', '', ''],
        ['', '', '']
      ],
      gameRun: [
        ['', '', ''],
        ['', '', ''],
        ['', '', '']
      ]
    }
  },
  created () {
    // this.socket = io('http://localhost:3000')
  },
  mounted () {
    // this.context = this.$refs.game.getContext('2d')
    // this.socket.on('position', data => {

    // })
  },
  methods: {
    move (direction) {
      this.socket.emit('move', direction)
    },
    mark (x, y) {
      this.gameRun[x][y] = 'X'
      console.log(this.gameRun)
      this.set(this.game, this.gameRun)
      // this.game = this.gameRun
      // this.game.splice(gameRun)
      // console.log(this.game)

    }
  }
}
</script>

<style scoped>
.hash {
  font-size: 50px;
  height: 600px;
  width: 600px;
}
.box {
  display: table-cell;
  vertical-align: middle;
  border: solid 1px #000;
  height: 200px;
  width: 200px;
}
</style>
