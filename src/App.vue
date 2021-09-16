<template>

    <div id="game">
        <square 
            :cnt="cnt"
            v-for="n of 9"
            :key="n"
            @click="click_action"
        />
    </div>

    <!-- @(v-on:)でクリックイベントを発生させる(カウンター) -->
    <!-- v-bindは（：）に省略可 -->
</template>


<script>
import square from './components/square.vue'
export default{
    name: 'App',
    data(){
        return{
            // クリック回数cntを０で初期化
            cnt:0,
        };
    },
    components: {
        square
    },
    methods:{
        click_action(){
            this.cnt++
            
        }
    }
};
</script>

<style >
#game{
    display: grid;
    grid-template-columns: 1fr 1fr 1fr;
    width: 450px;
}
</style>