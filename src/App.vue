<template>

    <div id="game">
        <square 
            :cnt="cnt"
            v-for="n of 9"
            :key="n"
            :number="n"
            @click="click_action"
            @cell_did="cell_did_event"
            @w_click="w_click_event"
        />
    </div>

    <!-- @(v-on:)でクリックイベントを発生させる(カウンター) -->
    <!-- v-bindは（：）に省略可 -->

    <!-- :keyにfor文で使った「nの値」を代入しているので、
                        :keyが各コンポーネントの番号を持っている -->
    <!-- keyでpropsを受け取ると不具合が起こるので、:numberで送る -->


<!-- 元のPG -->
    <!-- <square :cnt="cnt" @click="click_action" class="cell1"/>
    <square :cnt="cnt" @click="click_action" class="cell2"/>
    <square :cnt="cnt" @click="click_action" class="cell3"/>
    <square :cnt="cnt" @click="click_action" class="cell4"/>
    <square :cnt="cnt" @click="click_action" class="cell5"/>
    <square :cnt="cnt" @click="click_action" class="cell6"/>
    <square :cnt="cnt" @click="click_action" class="cell7"/>
    <square :cnt="cnt" @click="click_action" class="cell8"/>
    <square :cnt="cnt" @click="click_action" class="cell9"/> -->

</template>


<script>
import square from './components/square.vue'
export default{
    name: 'App',
    data(){
        return{
            // クリック回数cntを０で初期化
            cnt:0,
            // ゲームの状況を保存する配列
            states:[0,0,0,0,0,0,0,0,0]
        };
    },
    components: {
        square
    },
    methods:{
        click_action(){
            this.cnt++
        },
        cell_did_event(){

        },
        w_click_event(){
            this.cnt-- 
        }
    }
    // 子から受け取った情報を使うメソッドの作成
    // 各コンポーネントが○か✖かを表示
};
</script>

<style >
#game{
    display: grid;
    grid-template-columns: 1fr 1fr 1fr;
    width: 450px;
}
</style>