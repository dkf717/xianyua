<template>
  <el-popover trigger="click" placement="bottom" v-model="visible" :visible-arrow="false">
    <el-input placeholder="人数未定" :value="inputValue" slot="reference" @click="visible = !visible">
      <i slot="suffix" class="el-input__icon iconfont iconuser"></i>
    </el-input>

    <el-row type="flex">
      <el-col>每间</el-col>
      <el-col>
        <el-select size="mini" :value="adultNum + ' 成人'" @change="handleAudltChange">
          <el-option v-for="v in 7" :key="v" :value="v" />
        </el-select>
      </el-col>
      <el-col>
        <el-select size="mini" :value="childrenNum + ' 儿童'" @change="handleChildChange">
          <el-option v-for="v in childrenList" :key="v" :value="v" />
        </el-select>
      </el-col>
    </el-row>

    <el-row type="flex" justify="end" class="btn-col">
      <el-button size="mini" @click="onClick" type="primary">确定</el-button>
    </el-row>
  </el-popover>
</template>

<script>
export default {
  data() {
    return {
      visible: false,
      childrenList: [0, 1, 2, 3, 4],
      inputValue: null,
      num: [],
      adultNum: 1,
      childrenNum: 0,
      sum: 0
    };
  },
  methods: {
    onClick() {
      this.num = [this.adultNum, this.childrenNum];
      this.sum = this.adultNum + this.childrenNum;
      const world = ["成人", "儿童"];
      this.inputValue = this.num
        .filter(v => v > 0)
        .map((v, i) => `${v}${world[i]}`)
        .join(" ");
      this.visible = false;
      this.$emit("getperson",this.sum)
    },

    handleAudltChange(v) {
      this.adultNum = v;
    },

    handleChildChange: function(v) {
      this.childrenNum = v;
    }
  }
};
</script>

<style scoped lang="less">
.btn-col {
  margin-top: 20px;
  padding-top: 20px;
  border-top: 1px solid #ddd;
}
</style>

