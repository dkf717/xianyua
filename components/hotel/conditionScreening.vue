<template>
  <div>
    <!-- 目的地 -->
    <el-autocomplete
      v-model="searchForm.cityName"
      placeholder="目的地"
      value-key="name"
      :fetch-suggestions="querySearch"
      @select="handleCitySelect"
    />
    <!-- 入住时间 -->
    <el-date-picker
      v-model="searchForm.liveTime"
      :editable="false"
      :clearable="false"
      value-format="yyyy-MM-dd"
      type="daterange"
      range-separator="-"
      start-placeholder="入住日期"
      end-placeholder="离店日期"
      @change="onDateChange"
    />
    <!-- 人数 -->
    <PeopleNumber @getperson="getperson" style="display:inline-block" />
    <!-- 查看价格 -->
    <el-button type="primary" @click="onSubmit">查看价格</el-button>
  </div>
</template>

<script>
import PeopleNumber from "@/components/hotel/peopleNumber.vue";

export default {
  components: {
    PeopleNumber
  },
  data() {
    return {
      searchForm: {
        cityName: "南京",
        liveTime: [],
        person: 0
      }
    };
  },
  methods: {
    //获取目的地下拉列表
    async querySearch(v, cb) {
      if (!v) {
        return cb([]);
      }
      const res = await this.$axios({
        url: "/cities",
        params: {
          name: v
        }
      });
      const { data } = res.data;
      cb(data);
    },
    // 选中目的地选项触发
    handleCitySelect(v) {
      //   console.log(v);
      //   console.log(this.searchForm.cityName);
    },
    // 选择入住时间触发
    onDateChange(v) {
      //   console.log(v);
      //   console.log(this.searchForm.liveTime);
    },
    //获取人数
    getperson(num) {
      this.searchForm.person = num;
    },
    // 查看价格
    onSubmit() {
      // console.log(this.searchForm);
      this.$emit("getsearchForm", { ...this.searchForm });
    }
  }
};
</script>

<style>
</style>
