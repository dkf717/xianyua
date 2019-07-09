<template>
  <div class="win" style="margin-left:40px;">
    <div v-if="currentsize>=tal">
      <div v-for="(item,index) in guide" :key="index">
        <div v-if="item.images.length>=3" style="margin-bottom:20px; border-bottom:1px solid #ddd;">
          <p class="title">
            <a href="javascript:;" :src="item.title" @click="goTravel(item.id)">{{item.title}}</a>
          </p>
          <a href="javascript:;" @click="goTravel(item.id)">
            <p style="height:4em; font-size:14px;  overflow:hidden;" class="summary" v-html="item.summary"></p>
          </a>
          <!-- 这是主要内容 -->
          <el-row type="flex" class="row-bg" justify="space-between">
            <el-col :span="7.5" v-for="(item2,index2) in item.images" :key="index2">
              <div class="grid-content bg-purple" v-if="index2<3">
                <a href="javascript:;" @click="goTravel(item.id)">
                  <img :src="item2" alt style="width:220px; height:150px;  object-fit: cover" />
                </a>
              </div>
            </el-col>
          </el-row>
          <!-- 这是下面的小内容，流量，点赞数 -->
          <el-row type="flex" class="row-bg" justify="space-between" style="margin:20px 0px;">
            <el-col :span="7.5">
              <div class="grid-content bg-purple">
                <i class="iconfont icon-address fcolor" style="font-size:20px;" ></i>
                <span style="font-size:10px;" class="fcolor">{{item.cityName}}&nbsp;&nbsp;by</span>
                <a href>
                  <img
                    :src="'http://157.122.54.189:9095'+item.account.defaultAvatar"
                    alt
                    style="width:15px; height:15px;  object-fit: cover"
                  />
                  <span style="font-size:10px; color:orange;">{{item.account.nickname}}</span>
                </a>
                <i class="iconfont icon-keshi fcolor" style="font-size:20px;"></i>
                <span style="font-size:10px;" class="fcolor">{{item.watch}}</span>
              </div>
            </el-col>
            <el-col :span="7.5">
              <div class="grid-content bg-purple">
                <span style="color:orange">{{item.like||0}}赞</span>
              </div>
            </el-col>
          </el-row>
        </div>
        <!-- 这是一张图的情况的主要内容 -->
        <div v-else style="margin-bottom:10px; border-bottom:1px solid #ddd;">
          <el-row type="flex" class="row-bg" justify="space-between" >
            <!-- 图片 -->
            <el-col :span="7.5" v-for="(item2,index2) in item.images" :key="index2">
              <div class="grid-content bg-purple" v-if="index2<1">
                <a href="javascript:;" @click="goTravel(item.id)">
                  <img :src="item2" alt style="width:220px; height:150px;  object-fit: cover" />
                </a>
              </div>
            </el-col>

            <!-- 图片右边的文字内容 -->
            <el-col :span="7.5" style="margin-left:10px;">
              <p class="title">
                <a href="javascript:;" @click="goTravel(item.id)">{{item.title}}</a>
              </p>
              <a href="javascript:;" @click="goTravel(item.id)">
                <span class="summary swidth"
                  style="height:4em; font-size:14px; overflow:hidden; display:inline-block;"
                  v-html="item.summary"
                ></span>
              </a>
              <!-- 这是下面的小内容，流量，点赞数 -->
              <el-row type="flex" class="row-bg" justify="space-between" style="margin-bottom:20px; width:479px;">
                <el-col :span="7.5">
                  <div class="grid-content bg-purple" >
                    <i class="iconfont icon-address fcolor" style="font-size:20px;"></i>
                    <span style="font-size:10px;" class="fcolor">{{item.cityName}}&nbsp;&nbsp;by</span>
                    <a href>
                      <img
                        :src="'http://157.122.54.189:9095'+item.account.defaultAvatar"
                        alt
                        style="width:15px; height:15px;  object-fit: cover"
                      />
                      <span style="font-size:10px; color:orange;">{{item.account.nickname}}</span>
                    </a>
                    <i class="iconfont icon-keshi fcolor" style="font-size:20px;"></i>
                    <span style="font-size:10px;" class="fcolor">{{item.watch}}</span>
                  </div>
                </el-col>

                <el-col :span="7.5">
                  <div class="grid-content bg-purple">
                    <span style="color:orange">{{item.like||0}}赞</span>
                  </div>
                </el-col>
              </el-row>
            </el-col>
          </el-row>
        </div>
      </div>
    </div>
    <div v-else >
      <div v-for="(item,index) in guide" :key="index" >
        <div v-if="currentsize>=index+1" style="margin-bottom:20px; border-bottom:1px solid #ddd;">
          <div v-if="item.images.length>=3">
            <p class="title">
              <a href="javascript:;" @click="goTravel(item.id)">{{item.title}}</a>
            </p>
            <a href="javascript:;" @click="goTravel(item.id)">
              <p style="height:4em; font-size:14px;  overflow:hidden;" class="summary" v-html="item.summary"></p>
            </a>
            <!-- 这是主要内容 -->
            <el-row type="flex" class="row-bg" justify="space-between">
              <el-col :span="7.5" v-for="(item2,index2) in item.images" :key="index2">
                <div class="grid-content bg-purple" v-if="index2<3">
                  <a href="javascript:;" @click="goTravel(item.id)">
                    <img :src="item2" alt style="width:220px; height:150px;  object-fit: cover" />
                  </a>
                </div>
              </el-col>
            </el-row>
            <!-- 这是下面的小内容，流量，点赞数 -->
            <el-row type="flex" class="row-bg" justify="space-between" style="margin:20px 0px;">
              <el-col :span="7.5">
                <div class="grid-content bg-purple">
                  <i class="iconfont icon-address fcolor" style="font-size:20px;"></i>
                  <span style="font-size:10px;" class="fcolor">{{item.cityName}}&nbsp;&nbsp;by</span>
                  <a href>
                    <img
                      :src="'http://157.122.54.189:9095'+item.account.defaultAvatar"
                      alt
                      style="width:15px; height:15px;  object-fit: cover"
                    />
                    <span style="font-size:10px; color:orange">{{item.account.nickname}}</span>
                  </a>
                  <i class="iconfont icon-keshi fcolor" style="font-size:20px;"></i>
                  <span style="font-size:10px; " class="fcolor">{{item.watch}}</span>
                </div>
              </el-col>
              <el-col :span="7.5">
                <div class="grid-content bg-purple">
                  <span style="color:orange">{{item.like||0}}赞</span>
                </div>
              </el-col>
            </el-row>
          </div>
          <!-- 这是一张图的情况的主要内容 -->
          <div v-else>
            <el-row type="flex" class="row-bg" justify="space-between">
              <!-- 图片 -->
              <el-col :span="7.5" v-for="(item2,index2) in item.images" :key="index2">
                <div class="grid-content bg-purple" v-if="index2<1">
                  <a href="javascript:;" @click="goTravel(item.id)">
                    <img :src="item2" alt style="width:220px; height:150px;  object-fit: cover" />
                  </a>
                </div>
              </el-col>

              <!-- 图片右边的文字内容 -->
              <el-col :span="7.5" style="margin-left:10px;">
                <p class="title">
                  <a href="javascript:;" @click="goTravel(item.id)">{{item.title}}</a>
                </p>
                <a href="javascript:;" @click="goTravel(item.id)">
                  <span
                    style="height:4em; font-size:14px; overflow:hidden; display:inline-block;"
                    class="summary swidth"
                    v-html="item.summary"
                  ></span>
                </a>
                <!-- 这是下面的小内容，流量，点赞数 -->
                <el-row type="flex" class="row-bg" justify="space-between" style="margin-bottom:20px; width:479px;">
                  <el-col :span="7.5">
                    <div class="grid-content bg-purple">
                      <i class="iconfont icon-address fcolor" style="font-size:20px;"></i>
                      <span style="font-size:10px;" class="fcolor">{{item.cityName}}&nbsp;&nbsp;by</span>
                      <a href>
                        <img
                          :src="'http://157.122.54.189:9095'+item.account.defaultAvatar"
                          alt
                          style="width:15px; height:15px;  object-fit: cover"
                        />
                        <span style="font-size:10px; color:orange;">{{item.account.nickname}}</span>
                      </a>
                      <i class="iconfont icon-keshi fcolor" style="font-size:20px;"></i>
                      <span style="font-size:10px;" class="fcolor">{{item.watch}}</span>
                    </div>
                  </el-col>

                  <el-col :span="7.5">
                    <div class="grid-content bg-purple">
                      <span style="color:orange">{{item.like||0}}赞</span>
                    </div>
                  </el-col>
                </el-row>
              </el-col>
            </el-row>
          </div>
        </div>
      </div>
    </div>
    <div class="block">
      <el-pagination
        @size-change="handleSizeChange"
        @current-change="handleCurrentChange"
        :current-page="currentPage4"
        :page-sizes="pagesize"
        :page-size="3"
        layout="total, sizes, prev, pager, next, jumper"
        :total="tal"
      ></el-pagination>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      guide: [],
      tal: 0,
      // lpp:'',
      data: "",
      currentPage4: 1,
      currentsize: 0,
      pagesize: [3, 5, 10, 15]
    };
  },
  watch: {
    //监听变化
    $route() {
      // console.log(this.$route.query)
      // this.lpp =sessionStorage.getItem('city')
      this.tiaozhuan();
    }
  },
  methods: {
    goTravel: function(name) {
      this.$router.push({ path: "/post/detail?id=" + name });
    },
    tiaozhuan: function(number) {
      const { city } = this.$route.query;
      // console.log(city);
      this.$axios({
        url: city ? "/posts?city=" + city : "/posts",
        method: "GET"
      }).then(res => {
        const { data } = res.data;
        const { total } = res.data;
        this.tal = total;
        this.guide = data;
        this.guide = this.guide.slice(number);
      });
      console.log(this.currentsize);
    },
    handleSizeChange(val) {
      this.currentsize = val;
      this.tiaozhuan();
      console.log(`每页 ${val} 条`);
    },
    handleCurrentChange(val) {
      this.tiaozhuan((val - 1) * this.currentsize);
      console.log(`当前页: ${val}`);
    }
  },
  mounted: function() {
    // 请求推荐列表的数据
    this.tiaozhuan();
    this.currentsize = this.pagesize[0];
  }
};
</script>

<style scoped lang="less">
.el-row {
  // margin-bottom: 20px;
//   &:last-child {
//     margin-bottom: 0;
//   }
//   .row-bg {
//     // padding: 10px 0;
//     // background-color: #f9fafc;
//   }
  .title {
    margin-bottom: 15px;
    font-size: 18px;
    height: 21px;
    a {
        display: inline-block;
        height: 21px;
        text-overflow: ellipsis;
        overflow: hidden;
        white-space: nowrap;
        width: 496px;
    }
  }
  .title:hover > a {
    color: orange;
  }
  .summary{
      line-height:20px;
      color:#666;
      margin-bottom:20px;
  }
  .swidth{
      width:475px;
  }
  .fcolor{
      color:#999
  }
}
</style>
