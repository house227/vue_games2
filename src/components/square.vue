<template>
    <div class="cell" @click="action">
        <div> {{ square_cell }}</div>
    </div>

</template>

<script>
let cnt = 0;
export default{
name:'square',
props: {
    square_cell: String
},
mounted(){
    this.cnt = 1
},
methods:{
    action(){
        this.cnt++
        if(cnt % 2 !== 0){
            this.msg = '○'
        }else{
            this.msg = '✖'
        }
    }
}

}
</script>

<style>
.cell{
    border: 1px solid black;
    height: 200px;
    width: 200px;
    text-align: center;
    line-height: 90px;
    font-size: 30px;
}
</style>