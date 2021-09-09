<template>
    <div class="alert alert-info">
        <div v-on:click="action">{{ square }} {{ msg }}</div>
    </div>
</template>

<script>
export default{
name: 'square',
    props: {
        square:String
    },
    mounted(){
        this.cnt = 0;
    },
    methods:{
        action(){
            this.cnt++
            if(cnt % 2 !== 0){
                this.msg = '○'
            } else{
                this.msg = '✖'
            }
        }
    }

}
</script>
