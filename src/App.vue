<template>
    <square v-bind:square_cell="a" @click="action"/>
</template>

<script>

let cnt = 0;
import square from './components/square.vue'
export default{
    name: 'App',
    components: {
        square
    },
    methods:{
        action(){
            cnt++
            if(cnt % 2 !== 0){
            this.a = '○'
        }else{
            this.a = '✖'
        }
        }
    }

}
</script>
