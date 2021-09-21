<template>
    <div id="result_game"> {{ judge_result }}</div>
</template>

<script>

export default{
    name:"judge_game",
    props:{
        judge_result:String
    }
    
}
</script>

<style>
    #result_game{
        font-size: 60px;
        padding-left:150px;
    }
</style>