<template>
  <el-row :gutter="20">
    <el-col :span="8">
      <nuxt-link :to="'/hotel/' + hotelInfo.id + '.html'">
        <img :src="hotelInfo.photos" :alt="hotelInfo.name" width="320" height="210" />
      </nuxt-link>
    </el-col>
    <el-col :span="10">
      <!-- 名称信息 -->
      <h4>
        <nuxt-link :to="'/hotel/' + hotelInfo.id + '.html'">{{hotelInfo.name}}</nuxt-link>
      </h4>
      <div>
        <span>{{hotelInfo.alias}}</span>
        <!-- 星级展示 -->
        <StarLevel v-if="hotelInfo.hotellevel" :level="hotelInfo.hotellevel.level" />
        <span v-if="hotelInfo.hoteltype">{{hotelInfo.hoteltype.name}}</span>
      </div>

      <!-- 评价信息 -->
      <el-row type="flex" :gutter="10">
        <el-col :span="10">
          <el-rate
            v-model="hotelInfo.stars"
            disabled
            show-score
            text-color="#ff9900"
            score-template="{value}"
          ></el-rate>
        </el-col>
        <el-col :span="7">
          <span class="height-light">{{Math.floor(Math.random() * 100) + 1}}</span> 条评价
        </el-col>
        <el-col :span="7">
          <span class="height-light">{{Math.floor(Math.random() * 100) + 1}}</span> 篇游记
        </el-col>
      </el-row>

      <!-- 简介 -->
      <div class="hotel-summary-row">{{hotelInfo.summary}}</div>

      <div class="location-row">
        <iconFont class="iconlocation" />
        位于: {{hotelInfo.address}}
      </div>
    </el-col>

    <el-col :span="6" class="price-col">
      <el-table
        :data="hotelInfo.products"
        style="width: 100%"
        class="price-table"
        :show-header="false"
        row-class-name="product-row"
        @row-click="handleProductClick"
      >
        <el-table-column prop="name" />
        <el-table-column>
          <template slot-scope="scope">
            <span class="height-light larger">￥{{scope.row.price}}</span>起
            <i class="el-icon-arrow-right"></i>
          </template>
        </el-table-column>
      </el-table>
    </el-col>
  </el-row>
</template>
<script>
import StarLevel from "@/components/hotel/starLevel.vue";
export default {
  components: {
    StarLevel
  },
  props: ["hotelInfo"],
  mounted() {
    setTimeout(() => {
      console.log(33333, this.$props.hotelInfo);
    }, 1000);
  }
};
</script>

<style>
</style>
