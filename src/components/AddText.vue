<template>
  <div id="main">
    <textarea cols="20" rows="2" v-model="text"></textarea>
    <button @click="buttonClick ">Add Text</button>
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
  width: 200px;
  height: 150px;
  background-color: var(--switcher-bg);
  display: flex;
  flex-direction: column;
  align-items: center;
  padding-top: 20px;
  border: 1px solid black;
}
textarea{
  resize: none;
  outline: none;
  border-radius: 6px;
  padding: 5px;
}
button{
  width: 100px;
  height: 30px;
  border: none;
  border-radius: 6px;
  margin-top: 10px;
}
</style>