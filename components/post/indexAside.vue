<template>
  <div class="aside">
    <div class="border">
      <div class="item kuandu" v-for="(item,index) in cities" :key="index">
        {{item.type}}
        <i class="iconfont icon-jiantou"></i>
        <div class="dingwei">
          <div class="item xianshi" v-for="(item2,index) in item.children" :key="index">
            <a href="javascript:;" class="number" @click="goTravel(item2.city)">{{index+1}}</a>
            <a href="javascript:;" class="city" @click="goTravel(item2.city)">{{item2.city}}</a>
            <a href="javascript:;" class="introduct" @click="goTravel(item2.city)">{{item2.desc}}</a>
          </div>
        </div>
      </div>
    </div>
    <h4 class="line">推荐城市</h4>
    <a href="#">
      <img src="http://157.122.54.189:9093/images/pic_sea.jpeg" class="image" />
    </a>
  </div>
</template>

<script>
export default {
  data() {
    return {
      // isCollapse: true,
      cities: []
    };
  },
  methods: {
    goTravel: function(name) {
      // console.log(name)
      this.$router.push({ path: "/post?city=" + name });
      // sessionStorage.setItem('city',name)
    }
  },
  mounted() {
    // 请求推荐列表的数据
    this.$axios({
      url: "/posts/cities",
      method: "GET"
    }).then(res => {
      const { data } = res.data;
      const {total} =res.data;
      this.total=total;
      this.cities = data;
      // console.log(this.cities)
    });
  }
};
</script>

<style scoped lang="less">
.aside {
  width: 250px;
  .border {
    width: 250px;
    position: relative;
    .kuandu {
      border: 1px solid #ddd;
      border-bottom: none;
      height: 40px;
      line-height: 40px;
      padding-left: 10px;
      box-sizing: border-box;
      font-size: 14px;
      .iconfont {
        margin-left: 150px;
      }
      .dingwei {
        width: 320px;
        position: absolute;
        left: 250px;
        top: 0px;
        display: none;
        border: 1px solid #ddd;
        border-left: none;
        background-color: white;
        z-index: 99;
        .xianshi {
          height: 40px;
          line-height: 40px;
          padding-left: 10px;
          box-sizing: border-box;
          .number {
            font-style: italic;
            font-size: 20px;
            font-weight: 450;
            color: orange;
            margin-right: 10px;
          }
          .city {
            color: orange;
            margin-right: 10px;
          }
          .city:hover {
            text-decoration: underline;
          }
          .introduct {
            color: #999;
          }
          .introduct:hover {
            text-decoration: underline;
          }
        }
        .xianshi:last-of-type {
          border-left: 1px solid #ddd;
        }
      }
    }
    .kuandu:last-of-type {
      border-bottom: 1px solid #ddd;
    }
    .kuandu:hover > .dingwei {
      display: block;
    }
    .kuandu:hover {
      border-right: none;
      color: orange;
    }
  }
  .line {
    height: 60px;
    line-height: 80px;
    box-sizing: border-box;
    border-bottom: 1px solid #ddd;
    font-weight: 400;
  }
  .image {
    margin-top: 8px;
    width: 250px;
  }
}
</style>
