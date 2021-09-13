<template>
    <div class="cell" @click="action">
       <p>{{ msg }}</p> 
    </div>

</template>

<script>

export default{
name:'square',
props: {
    msg: String
},
mounted(){
    this.cnt = 0
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
