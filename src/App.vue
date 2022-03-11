<template>
  <div>
    <Search></Search>
    <MyTab></MyTab>
  </div>
</template>

<script>
import Search from '@/components/Search'
import MyTab from '@/components/MyTab'

export default {
  name: 'App',
  components:{
    Search,
    MyTab
  }
}
</script>

<style lang="less">

</style>
