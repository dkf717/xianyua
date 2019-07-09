<template>
<el-row>
    <el-col :span="6">
      <IndexAside/>
    </el-col>
    <el-col :span="18" class="rig">
      <IndexSearch/>
      <IndexMain/>
    </el-col>
</el-row>
</template>

<script>
import IndexAside from "@/components/post/indexAside.vue"
import IndexSearch from "@/components/post/indexSearch.vue"
import IndexMain from "@/components/post/indexMain.vue"
export default {
    components:{
        IndexAside,
        IndexSearch,
        IndexMain
    }
}
</script>

<style scoped lang="less">
  .el-row {
    width:1000px;
    margin:20px auto;
  }
  .bg-purple-light {
    background: #e5e9f2;
  }
  .grid-content {
    min-height: 36px;
  }
</style>
