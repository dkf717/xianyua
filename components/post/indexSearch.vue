<template>
  <div style="margin-left:40px;">
    <el-input placeholder="请输入想去的地方，比如：‘广州’" v-model="input3" class="input-with-select">
      <el-button slot="append" icon="el-icon-search" @click="goTravel(input3)"></el-button>
    </el-input>
    <div class="wenzi">
      <span>推荐:</span>
      <a href="javascript:;" class="city" @click="goTravel('广州')">广州</a>
      <a href="javascript:;" class="city" @click="goTravel('上海')">上海</a>
      <a href="javascript:;" class="city" @click="goTravel('北京')">北京</a>
    </div>
    <el-row type="flex" class="row-bg" justify="space-between">
      <el-col :span="3">
        <div class="grid-content bg-purple">
          <span class="gonglue">推荐攻略</span>
        </div>
      </el-col>
      <el-col :span="3">
        <div class="grid-content bg-purple">
          <el-button class="btn" type="primary" icon="el-icon-edit" @click="goWrite()">写游记</el-button>
        </div>
      </el-col>
    </el-row>
  </div>
</template>

<script>
export default {
  data() {
    return {
      input3: ""
    };
  },
  methods: {
    goTravel: function(name) {
      // console.log(name)
      this.$router.push({ path: "/post?city=" + name });
      // sessionStorage.setItem('city',name)
    },
    goWrite: function() {
      // console.log(name)
      this.$router.push({ path: "/post/create" });
      // sessionStorage.setItem('city',name)
    }
  }
};
</script>

<style scoped lang="less">
.wenzi {
  color: #666;
  font-size: 12px;
  margin-top: 10px;
  .city {
    color: #666;
    margin-left: 10px;
  }
  .city:hover {
    color: orange;
    text-decoration: underline;
  }
}
.el-row {
  margin-bottom: 20px;
  .grid-content {
    min-height: 36px;
    .gonglue {
      display: inline-block;
      height: 55px;
      line-height: 55px;
      border-bottom: 3px solid orange;
      color: orange;
      font-size: 18px;
    }
    .btn {
      margin-top: 10px;
    }
  }
  .row-bg {
    padding: 0px 18px 0px 0px;
    border-bottom: 1px solid #ddd;
  }
}
</style>
