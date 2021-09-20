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
            @game_data="game_data"
        />
    </div>

    <!-- @(v-on:)でクリックイベントを発生させる(カウンター) -->
    <!-- v-bindは（：）に省略可 -->

    <!-- :keyにfor文で使った「nの値」を代入しているので、
                    :keyが各コンポーネントの番号を持っている -->
    <!-- keyでpropsを受け取ると不具合が起こるので、:numberで送る  -->


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
            status:[0,0,0,0,0,0,0,0,0],
            lines:[
                // 横ライン
                [status[0], status[1], status[2]],
                [status[3], status[4], status[5]],
                [status[6], status[7], status[8]]
            ],
            result:'no data'
        };
    },
    components: {
        square
    },
    methods:{
        // クリックイベント。全体のクリック数を++
        click_action(){
            this.cnt++
        },

        // セルに○/✖が入った時のイベント(emit)
        cell_did_event(con_number, num){
            // ゲーム状況を記録するステータス配列に〇(1)か×(-1)かを入れる
            this.status[--con_number] = num
            // ライン配列に値を代入する
        },

        // 同じ場所をクリックされた時のイベント。全体のクリック数を--
        w_click_event(){
            this.cnt-- 
        },

        //ライン配列にステータスを随時追加していく 
        game_data(){
            let result_cnt = 0;
            let x = 0;
            for(let i = 0; i < this.lines.length; i++){
                for(let j = 0; j < this.lines[i].length; j++){
                    this.lines[i][j] = this.status[x++];
                    // console.log("ライン配列" + this.lines[0])
                }
            }
                
            //配列の状況をforで回して確認し、勝敗を判定する
            //引き分けなら？
            for(let i = 0; i <this.lines.length; i++){
                let total = 0;
                for(let j = 0; j < this.lines[i].length; j++){
                    total += this.lines[i][j];
                    if(total === 3){
                        console.log('〇 is Win');
                        this.result = '〇';
                    }else if(total === -3){
                        console.log('✖ is Win');
                        this.result = '✖';
                    }
                }
            }
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

/* {x_line1: [status[0], status[1], status[2]]},
{x_line2: [status[3], status[4], status[5]]},
{x_line3: [status[6], status[7], status[8]]},
// 縦ライン
{y_line1: [status[0], status[3], status[6]]},
{y_line2: [status[1], status[4], status[7]]},
{y_line3: [status[2], status[5], status[8]]},
// 斜めライン
{z_line1: [status[0], status[4], status[8]]},
{z_line2: [status[2], status[4], status[6]]} */

</style>

