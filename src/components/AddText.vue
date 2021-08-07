<template>
  <div id="main">
    <textarea cols="20" rows="2" v-model="text"></textarea>
    <button @click="buttonClick ">Add Text</button>
    <div id="wrapper">
      <div id="spanwrapper">
        <span :style="textStyle">A</span> 
      </div>
      <vue-slider
      :min=8
      :max=24
      v-model="textSize"
      :tooltip="'none'"
      :width=120>
      </vue-slider>
    </div>
  </div>
</template>

<script>
export default {
  name: 'AddText',
  data() {
    return {
      text: '',
      textSize: this.markerTextSize
    }
  },
  props: [ 'markerTextSize' ],
  methods: {
    buttonClick() {
      this.$emit('add-text', [this.text, this.textSize]);
    }
  },
  computed: {
    textStyle () {
      return {
        fontSize: `${this.textSize}pt`,
      }
    }
  }
}

</script>

<style scoped>
#main{
  width: 200px;
  height: 160px;
  background-color: var(--switcher-bg);
  display: flex;
  flex-direction: column;
  align-items: center;
  padding-top: 20px;
}
textarea{
  resize: none;
  outline: none;
  border-radius: 6px;
  padding: 5px;
  border: 1px solid white;
}
button{
  width: 100px;
  height: 30px;
  border: 1px solid white;
  color: white;
  background-color: var(--switcher-bg);
  border-radius: 6px;
  margin-top: 10px;
}
button:hover{
  box-shadow: inset 0 0 5px lightgrey;
}
span{
  padding-right: 10px;
}
#wrapper{
  display: flex;
  flex-direction: row;
  align-items: center;
  justify-content: space-between;
  
  margin-top: 15px;
  height: 30px;
  width: 160px;
}
#spanwrapper{
  display: flex;
  flex-direction: row;
  align-items: center;
  justify-content: center;

}
</style>