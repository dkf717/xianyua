<template>
  <div>
    <el-row :gutter="50">
      <el-col :span="6">
        <el-row type="flex" justify="space-between">
          <span>价格</span>
          <span>0-{{scenic}}</span>
        </el-row>
        <el-row>
          <el-col>
            <el-slider v-model="scenic" :min="0" :max="4000" @change="scenicChange"></el-slider>
          </el-col>
        </el-row>
      </el-col>
      <el-col :span="18">
        <el-row>
          <el-col :span="6" v-for="(v,i) in hotelConditionsKey" :key="i">
            <HotelConditions
              :hotelConditionsKey="hotelConditionsKey[i]"
              :hotelConditions="hotelConditions[hotelConditionsKey[i]]"
              @getCheckList="getCheckList"
            />
          </el-col>
        </el-row>
      </el-col>
    </el-row>
  </div>
</template>

<script>
import HotelConditions from "@/components/hotel/hotelConditions.vue";
export default {
  components: {
    HotelConditions
  },
  data() {
    return {
      scenic: 4000,
      hotelConditions: {},
      hotelConditionsKey: ["levels", "types", "assets", "brands"],
      checkList: { price_lt: "4000", levels: [], types: [], assets: [], brands: [] }
    };
  },
  methods: {
    getCheckList(v) {
      this.checkList[v.type] = [...v.checkList];
      this.$emit("getCheckList", this.checkList);
    },
    scenicChange(v) {
      this.checkList.price_lt = v;
      this.$emit("getCheckList", this.checkList);
    }
  },
  mounted() {
    this.$axios({
      url: "hotels/options"
    }).then(res => {
      this.hotelConditions = res.data.data;
    });
  }
};
</script>
<style>
.scenic {
  width: 200px;
}
</style>
