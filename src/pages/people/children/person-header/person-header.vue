<template>
    <div class="person-header">
      <bg-img></bg-img>
      <person-info></person-info>
    </div>
</template>

<script>
  import bgImg from './children/bgImg'
  import personInfo from './children/person-info'
    export default {
        name: "person-header",
        data() {
            return {}
        },
      components:{
        bgImg,
        personInfo
      }
    }
</script>

<style lang="stylus" scoped>
.person-header
  width: 100%
  /*height:20rem*/
  background: #ffffff;
  box-sizing border-box
  padding-bottom 1.1rem
  /*background: thistle*/
</style>
