<template>
    <div class="my-article">
      <div class="action-guide">
        <span class="my-action">我的文章</span>
      </div>
      <my-article></my-article>
    </div>
</template>

<script>
  import myArticle from './template-file/tem-article'
    export default {
        name: "article",
        data() {
            return {}
        },
        components:{
          myArticle
        }
    }
</script>

<style lang="stylus" scoped>
.my-article
  .action-guide
    border-bottom 1px solid #f6f6f6
    .my-action
      display inline-block
      padding .9rem 0
      font-weight 600
      color: #1a1a1a
      font-size .9375rem
</style>
