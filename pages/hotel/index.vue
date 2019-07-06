<template>
  <div>
    <!-- 面包屑导航 -->
    <el-breadcrumb separator-class="el-icon-arrow-right">
      <el-breadcrumb-item>酒店</el-breadcrumb-item>
      <el-breadcrumb-item>{{cityName}}酒店预订</el-breadcrumb-item>
    </el-breadcrumb>
    <!-- 输入条件筛选 -->
    <ConditionScreening />
  </div>
</template>

<script>
import ConditionScreening from "@/components/hotel/conditionScreening.vue";
export default {
  components: {
    ConditionScreening
  },
  data() {
    return {
      //城市ID
      cityId: 0,
      //诚实名字
      cityName: ""
      //入住时间
    };
  },
  methods: {
    getCityListByName(name, cb) {
      this.$axios({
        url: "cities?name=" + name
      }).then(res => {
        var query = { ...this.$route.query };
        this.cityName = res.data.data[0].name;
        query.city = this.cityId = res.data.data[0].id;
        this.$router.push({ path: "hotel", query });
      });
    },
    handleSelect(item) {
      console.log(item);
    }
  },
  mounted() {
    this.getCityListByName("南京市");
  }
};
</script>
<style>
</style>
