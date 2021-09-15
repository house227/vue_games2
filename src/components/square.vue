<template>
<!-- マスに@(v-on:)でクリックイベント追加 -->
    <div class="cell" @click="action">
        <div> {{ square_cell }}</div>
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
        key: Number
    },
    mounted(){
        // 子特有のカウンターをブラウザ起動時に０で初期化
        this.bit_cnt = 0
    },
    methods:{
        // クリックイベント
        action(){
            // 親から受け取ったクリック回数を元に条件分岐
            // 子特有のカウンターbit_cntですでにクリックしたかを確認
            // クリックされていればカウントが１なので条件が通らない。
            if(this.cnt % 2 === 0 && this.bit_cnt === 0){
                this.square_cell = "〇";
                this.bit_cnt++
            }else if(this.cnt % 2 !== 0 && this.bit_cnt === 0){
                this.square_cell = "✖";
                this.bit_cnt++
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