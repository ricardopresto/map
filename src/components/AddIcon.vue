<template>
    <div>
        <div id='main'>
            <Icon v-for="icon in iconlist" :key="icon.name" :image="icon.image"/>
        </div>    
    </div>
</template>

<script>

import Icon from './Icon.vue';
export default {
    name: 'AddIcon',
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
    height: 400px;
    margin-left: 20px;
    border: 1px solid black;
}
</style>