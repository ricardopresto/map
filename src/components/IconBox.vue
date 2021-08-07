<template>
    <div id='main'>
        <Icon 
        v-for="icon in iconlist" 
        :key="icon.index" 
        :image="icon.image" 
        @icon-click="$emit('icon-click', $event)"/>
    </div>    
</template>

<script>

import Icon from './Icon.vue';
export default {
    name: 'IconBox',
    components: {
        Icon
    },
    props: ['iconlist'],
    data() {
        return {

        }

    }
}
</script>

<style scoped>
#main{
    width: 200px;
    height: 160px;
    display: flex;
    flex-flow: row wrap;
    background-color: var(--switcher-bg);
}
</style>