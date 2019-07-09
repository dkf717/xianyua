<template>
  <div style="width:1000px; margin:0 auto">
    <!-- 面包屑导航 -->
    <el-breadcrumb separator-class="el-icon-arrow-right">
      <el-breadcrumb-item>酒店</el-breadcrumb-item>
      <el-breadcrumb-item>{{cityName}}酒店预订</el-breadcrumb-item>
    </el-breadcrumb>
    <!-- 输入条件筛选 -->
    <ConditionScreening @getsearchForm="getsearchForm" />
    <!-- 地图 -->
    <Map :scenics="scenics" />
    <!-- 选择条件筛选 -->
    <OptionsScreen @getCheckList="getCheckList" />
    <!-- 酒店展示 -->
    <HotelDisplay v-for="v in hotelList" :key="v.id" :hotelInfo="v" />
    <el-input v-model="urlParameter" placeholder="请输入内容" v-show="false" />
  </div>
</template>

<script>
import ConditionScreening from "@/components/hotel/conditionScreening.vue";
import Map from "@/components/hotel/map.vue";
import OptionsScreen from "@/components/hotel/optionsScreen.vue";
import HotelDisplay from "@/components/hotel/hotelDisplay.vue";
export default {
  components: {
    ConditionScreening,
    Map,
    OptionsScreen,
    HotelDisplay
  },
  data() {
    return {
      //城市ID
      cityId: 74,
      //诚实名字
      cityName: "",
      //条件搜索数据
      searchForm: {
        liveTime: []
      },
      //城市标记
      scenics: [],
      // 条件选项数据
      checkList: {
        price_lt: "",
        levels: [],
        types: [],
        assets: [],
        brands: []
      },
      //酒店数据
      hotelList: []
    };
  },
  methods: {
    getCityListByName(name) {
      this.$axios({
        url: "cities?name=" + name
      }).then(res => {
        this.scenics = res.data.data[0].scenics;
        var query = { ...this.$route.query };
        this.cityName = res.data.data[0].name;
        query.city = this.cityId = res.data.data[0].id;
        this.$router.push({ path: "hotel", query });
      });
    },
    // 获取条件搜索数据
    getsearchForm(v) {
      this.searchForm = v;
      this.$router.push({
        path: `hotel?city=${this.searchForm.cityName}${
          this.searchForm.liveTime.length === 0
            ? ""
            : "&enterTime=" +
              this.searchForm.liveTime[0] +
              "&leftTime=" +
              this.searchForm.liveTime[1]
        }`
      });
      this.getCityListByName(this.searchForm.cityName);
    },
    // 获取条件选项数据
    getCheckList(v) {
      this.checkList = { ...v };
    }
  },
  mounted() {
    this.getCityListByName("南京市");
  },
  computed: {
    urlParameter() {
      //拼接住宿时间
      const { liveTime } = this.searchForm;

      const liveTimeText = liveTime.length
        ? `&enterTime=${liveTime[1]}&leftTime=${liveTime[1]}`
        : "";
      // 拼接住宿价格
      const { price_lt } = this.checkList;
      const price_lt_text = price_lt ? `price_lt=${price_lt}` : "";
      // 拼接住宿等级
      const { levels } = this.checkList;
      const levelsText = levels.map(v => `&hotellevel_in=${v}`).join("");
      // 拼接住宿类型
      const { types } = this.checkList;
      const typesText = types.map(v => `&hoteltype_in=${v}`).join("");
      // 拼接酒店设施
      const { assets } = this.checkList;
      const assetsText = assets.map(v => `&hotelasset_in=${v}`).join("");
      // 拼接酒店品牌
      const { brands } = this.checkList;
      const brandsText = brands.map(v => `&hotelbrand_in=${v}`).join("");
      // 拼接参数
      const Parameter = `&city=${this.cityId}${liveTimeText}${price_lt_text}${levelsText}${typesText}${assetsText}${brandsText}`;
      //返回参数
      this.$axios({
        url: "/hotels/?" + Parameter
      }).then(res => {
        this.hotelList = res.data.data;
      });
      return Parameter;
    }
  }
};
</script>
<style>
</style>
