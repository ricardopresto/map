<template>
  <div id="main">
    <textarea name="" id="" cols="20" rows="2" v-model="text"></textarea>
    <button @click="buttonClick ">ADD</button>
  </div>
</template>

<script>
export default {
  name: 'AddText',
  data() {
    return {
      text: ''
    }
  },
  methods: {
    buttonClick() {
      console.log(this.text);
      this.$emit('add-text', this.text);
    }
  }
}

</script>

<style scoped>
#main{
  width: 150px;
  height: 150px;
  border: 1px solid black;
}
</style>