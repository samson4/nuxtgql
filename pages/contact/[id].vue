<template>
<h1>{{ id }}</h1>
</template>


<script>
export default{
    data(){
        return{
            id,
        }
    },
    created(){
        this.id=this.$route.params.id
    }
}

</script>