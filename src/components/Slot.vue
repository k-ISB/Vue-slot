<template>
  <div class="slot">
    <p id="slot">
        <input v-for="img in imgs" :key="img" type="button" value="." v-on:click="setImage(img)">
        <br>
        <img v-for="(image, index) of limitCount" :key="index" :src=image :id="imgs[index]">
    </p>
    <p id="clear" v-if="clear">おめでとう！100万円だ！！</p>
  </div>
</template>

<script>
export default {
  name: 'Slot',
  data: function() {
    return {
      clear: false,
      num: [0,1,2],
      imgs: ['img1','img2','img3'],
      images: [
        require('../assets/f0.png'),
        require('../assets/f1.png'),
        require('../assets/f2.png'),
        require('../assets/f3.png'),
        require('../assets/f4.png'),
        require('../assets/f5.png')
      ]
    };
  },
  computed: {
    limitCount() {
      return this.images.slice(0,3)
     } 
    },
  methods: {
    setImage: function(id) {
      //画像のランダム表示
      var i = parseInt(Math.random() * 5);
      document.getElementById(id).src = this.images[i];
      //絵柄が揃ったときの処理
      var slot = document.getElementById('slot');
      var btn = slot.getElementsByTagName('img');
      if(btn[0].src === btn[1].src && btn[0].src === btn[2].src){
        this.clear = true;
      }else{
        this.clear = false;
      }
    }
  }
}
</script>

<style scoped>
p{
    text-align: center;
}
input{
    font-size: 50px;
    margin-bottom: 20px;
    padding: 0 30px;
    border-radius: 8px;
}
#clear{
    color: brown;
    font-size: large;
    padding-top: 20px;
}
</style>