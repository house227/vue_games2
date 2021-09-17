<template>
<!-- マスに@(v-on:)でクリックイベント追加 -->
    <div class="cell" @click="action">
        <div style="font-size: 100px"> {{ square_cell }}</div>
    </div>

</template>

<script>
export default{
    name:'square',
    data(){
        return{
            square_cell:" ",
        };
    },
        // 親から送られてきたクリック回数をNumber型で受け取る
    props: {
        cnt: Number,
        // 親のkeyから各コンポーネントの番号を受け取る
        number: Number
    },
    mounted(){
        // 子特有のカウンターをブラウザ起動時に０で初期化
        this.click_cnt = 0

    },
    methods:{
        // クリックイベント
        action(){
            // コンポーネントの番号が受け取れてるかのテスト
            
            // 二度押時に全体のカウントを下げるemit
            if(this.click_cnt === 1){
                this.$emit('w_click')
            }

            // 親から受け取ったクリック回数を元に条件分岐
            // 子特有のカウンターbit_cntですでにクリックしたかを確認
            // クリックされていればカウントが１なので条件が通らない。
            if(this.cnt % 2 === 0 && this.click_cnt === 0){
                this.square_cell = "〇";
                // 自分がクリックされた事を親へ送るemit
                this.$emit('cell_did',this.number, 1)
                this.click_cnt++
                
            }else if(this.cnt % 2 !== 0 && this.click_cnt === 0){
                this.square_cell = "✖";
                this.$emit('cell_did',this.number, -1)
                this.click_cnt++
            }
        },
    },
};
</script>

<style>
/* マスの枠デザイン */
.cell{
    border: 1px solid black;
    height: 200px;
    width: 200px;
    text-align: center;
    line-height: 90px;
    font-size: 30px;
    padding-top: 50px;
}
</style>