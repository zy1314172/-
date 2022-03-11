<template>
  <div>
      Search <input type="text" v-model="message" @keyup="search">
  </div>
</template>

<script>
export default {
    name:'Search',
    data(){
        return {
            message:''
        }
    },
    methods:{
        search(){
            this.$bus.$emit('searchUser',this.message)
        }
    }
}
</script>

<style>

</style>