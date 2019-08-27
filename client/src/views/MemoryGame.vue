<template>
  <div>
    <button @click="zera">COMEÇAR</button>
    <div class="content">
      <div
        v-for="(item, index) in test"
        :key="index"
        class="box"
        @click="validOption(item,index)"
      >
        <img v-if="item.position" src="../assets/card_backside.jpg" width="200">
        <!-- <img v-else :src="'../assets/'+item.versa"> -->
        <img v-else src="../assets/logo.png" >
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'GameMemory',
  props: {

  },
  data(){
    return {
      test:[
        {
          'id':'01',
          'versa': 'logo.png',
          'position':true
        },
        {
          'id':'02',
          'versa': 'logo.png',
          'position':true
        },
        {
          'id':'03',
          'versa': 'logo.png',
          'position':true
        },
        {
          'id':'04',
          'versa': 'logo.png',
          'position':true
        },
        {
          'id':'01',
          'versa': 'logo.png',
          'position':true
        },
        {
          'id':'02',
          'versa': 'logo.png',
          'position':true
        },
        {
          'id':'03',
          'versa': 'logo.png',
          'position':true
        },
        {
          'id':'04',
          'versa': 'logo.png',
          'position':true
        },
      ],
      tentativa1:'',
      tentativa2:''
    }
  },
  computed: {

  },
  methods:{
    zera() {
      this.test = [
        {
          'id':'01',
          'versa': 'logo.png',
          'position':true
        },
        {
          'id':'02',
          'versa': 'logo.png',
          'position':true
        },
        {
          'id':'03',
          'versa': 'logo.png',
          'position':true
        },
        {
          'id':'04',
          'versa': 'logo.png',
          'position':true
        },
        {
          'id':'01',
          'versa': 'logo.png',
          'position':true
        },
        {
          'id':'02',
          'versa': 'logo.png',
          'position':true
        },
        {
          'id':'03',
          'versa': 'logo.png',
          'position':true
        },
        {
          'id':'04',
          'versa': 'logo.png',
          'position':true
        },
      ]
    },
    validOption(item, index){
      if(item.position){
        item.position = false

        if(this.tentativa1 === ''){
          this.tentativa1 = item
          this.tentativa1.index = index
          return;
        }else{
          this.tentativa2 = item
          this.tentativa2.index = index
        }

        if (this.tentativa1 != '' && this.tentativa2 != ''){
          if (this.tentativa1.id === this.tentativa2.id){
            this.tentativa2 = ""
            this.tentativa1 = ""
            return;
          }
          setTimeout(() => {
            this.test[this.tentativa1.index].position = true
            this.test[this.tentativa2.index].position = true
            this.tentativa1 = ""
            this.tentativa2 = ""
            return;
          },300);
        }

      }
    }

  }

}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
.box {
  display: inline-block;
  width: 200px;
  margin: 10px 30px;
  vertical-align: middle;
}
.content {
  width: 1200px;
  height: 1200px;
}
</style>
