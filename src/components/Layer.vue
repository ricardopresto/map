<template>
  <div id='layer' @click="setVisible">
    <span>{{ layerName }}</span>
    <i class="far fa-eye" v-if="visible"></i>
    <i class="far fa-eye-slash" v-if="!visible"></i>
  </div>
</template>

<script>

export default {
  name: 'Layer',
  props: ['layerID', 'layerName'],
  data() {
    return {
      visible: true
    }
  },
  methods: {
    setVisible() {
      this.visible = !this.visible;
      this.$emit("set-visible", [this.layerID, this.visible]);
    }
  }
}

</script>

<style scoped>
#layer{
  width: 198px;
  height: 40px;
  border: 1px solid red;
  color: white;
  display: flex;
  flex-direction: row;
  align-items: center;
  justify-content: space-between;
  padding: 10px;
}
</style>