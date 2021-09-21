<template>

    <div id="game">
        <square 
            :cnt="cnt"
            v-for="n of 9"
            :key="n"
            :number="n"
            @click="click_action"
            @cell_game="cell_game_event"
            @w_click="w_click_event"
        />
    </div>
        <judge_game :judge_result="result" />

    <!-- @(v-on:)でクリックイベントを発生させる(カウンター) -->
    <!-- v-bindは（：）に省略可 -->

    <!-- :keyにfor文で使った「nの値」を代入しているので、
                    :keyが各コンポーネントの番号を持っている -->
    <!-- keyでpropsを受け取ると不具合が起こるので、:numberで送る  -->
</template>


<script>
import square from './components/square.vue'
import judge_game from './components/judge_game.vue'

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
            result:'',
            judge:0
        };
    },
    components: {
        square,
        judge_game
    },
    methods:{
        // クリックイベント。全体のクリック数を++
        click_action(){
            this.cnt++
        },

        // セルに○/✖が入った時のイベント(emit)
        cell_game_event(con_number, num){
            this.judge++
            // ゲーム状況を記録するステータス配列に〇(1)か×(-1)かを入れる
            this.status[--con_number] = num
            
            //ライン配列にステータスを随時追加していく 
            let x = 0;
            for(let i = 0; i < this.lines.length; i++){
                for(let j = 0; j < this.lines[i].length; j++){
                    this.lines[i][j] = this.status[x++];
                    // console.log("ライン配列" + this.lines[0])
                }
            }
            for(let i = 0; i <this.lines.length; i++){
            //横列用変数
            let total_yoko = 0;
            //縦列用変数
            let total_tate = 0;
            //斜め用変数
            let total_naname1 = 0;
            let total_naname2 = 0;

            //横配列の状況をforで回して確認し、勝敗を判定する
            for(let j = 0; j < this.lines[i].length; j++){
                total_yoko += this.lines[i][j];
                total_tate += this.lines[j][i];
                total_naname1 = (this.lines[0][0] + this.lines[1][1] + this.lines[2][2]);
                total_naname2 = (this.lines[0][2] + this.lines[1][1] + this.lines[2][0]);
            }
            //〇が勝つ判定
            if((total_yoko === 3 || total_tate === 3 || total_naname1 === 3 || 
                total_naname2 === 3) && this.result === ''){
                console.log('〇 is Win');
                this.result = '〇の勝ち！';
                //✖が勝つ判定
            }else if((total_yoko === -3 || total_tate === -3 || total_naname1 === -3 ||
                    total_naname2 === -3) && this.result === ''){
                console.log('✖ is Win');
                this.result = '✖の勝ち！';
            }//引き分け
            if(this.judge === 9 && this.result === ''){
                console.log('引き分け');
                this.result('drow');
            }
        }
        },

        // 同じ場所をクリックされた時のイベント。全体のクリック数を--
        w_click_event(){
            this.cnt-- 
        },
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

