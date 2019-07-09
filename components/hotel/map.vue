<template>
  <div>
    <el-row type="flex">
      <el-col :span="16">
        <el-row type="flex">
          <el-col :span="3">区域：</el-col>
          <el-col :class="{'hidden-all': !show}">
            <div class="scenics-box">
              <a href="#" :class="{'location-budget': 1, active: !value}">全部</a>
              <a
                href="#"
                :class="{'location-budget': true, active: value === v.id}"
                v-for="v in scenics"
                :key="v.id"
              >{{v.name}}&nbsp;&nbsp;&nbsp;</a>
            </div>
            <a href="#">
              <i class="el-icon-d-arrow-right" />
              等{{scenics.length}}个区域
            </a>
          </el-col>
        </el-row>
        <el-row type="flex" class="option-row">
          <el-col :span="3">攻略:</el-col>
          <el-col>北京，你想要的都能在这找到。博古通今，兼容并蓄，天下一城，如是帝都。 景点以故宫为中心向四处辐射；地铁便宜通畅，而且覆盖绝大多数景点。 由于早上有天安门升旗仪式，所以大多数人选择在天安门附近住宿。</el-col>
        </el-row>
        <el-row type="flex">
          <el-col :span="3">
            均价
            <el-tooltip content="等级均价由平日价格计算得出，节假日价格会有上浮。" placement="top-start">
              <sup class="question-mark">?</sup>
            </el-tooltip>：
          </el-col>
          <el-col>
            <el-row type="flex" justify="start">
              <el-col :span="6">
                <el-tooltip
                  placement="bottom-start"
                  :visible-arrow="false"
                  content="等级评定是针对房价，设施和服务等各方面水平的综合评估。"
                >
                  <span>
                    <i class="iconfont iconhuangguan" v-for="v in 3" :key="v"></i>
                    <span class="price-budget">¥332</span>
                  </span>
                </el-tooltip>
              </el-col>
              <el-col :span="6">
                <el-tooltip
                  placement="bottom-start"
                  :visible-arrow="false"
                  content="等级评定是针对房价，设施和服务等各方面水平的综合评估。"
                >
                  <span>
                    <i class="iconfont iconhuangguan" v-for="v in 4" :key="v"></i>
                    <span class="price-budget">¥521</span>
                  </span>
                </el-tooltip>
              </el-col>
              <el-col :span="6">
                <el-tooltip
                  placement="bottom-start"
                  :visible-arrow="false"
                  content="等级评定是针对房价，设施和服务等各方面水平的综合评估。"
                >
                  <span>
                    <i class="iconfont iconhuangguan" v-for="v in 5" :key="v"></i>
                    <span class="price-budget">¥768</span>
                  </span>
                </el-tooltip>
              </el-col>
            </el-row>
          </el-col>
        </el-row>
      </el-col>
      <el-col :span="8">地图</el-col>
    </el-row>
  </div>
</template>
<script>
export default {
  props: ["scenics"],
  data() {
    return {
      value: 0,
      show: false
    };
  },
  mounted() {}
};
</script>

<style>
.iconhuangguan {
    color: #f90;
  }
</style>
