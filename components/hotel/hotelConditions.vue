<template>
  <div>
    <p>{{hotelConditionsKey | key}}</p>
    <el-dropdown @command="hanldeChange">
      <span class="el-dropdown-link">
        {{checkList | text}}
        <i class="el-icon-arrow-down el-icon--right"></i>
      </span>
      <el-dropdown-menu slot="dropdown">
        <el-dropdown-item v-for="v in hotelConditions" :key="v.id" :command="
        v.id">
          <i class="iconfont iconcircle" v-if="checkList.indexOf(v.id)===-1" />
          <i class="iconfont iconright-1" v-else />
          {{v.name}}
        </el-dropdown-item>
      </el-dropdown-menu>
    </el-dropdown>
  </div>
</template>

<script>
export default {
  props: ["hotelConditionsKey", "hotelConditions"],
  filters: {
    key(key) {
      return key === "levels"
        ? "住宿等级"
        : key === "types"
        ? "住宿类型"
        : key === "assets"
        ? "酒店设施"
        : "酒店品牌";
    },
    text(v) {
      return v.length ? `已选${v.length}项` : "不限";
    }
  },
  data() {
    return {
      checkList: [
         
      ]
    };
  },
  methods: {
    hanldeChange(v) {
      //   console.log(v);
      const index = this.checkList.indexOf(v);
      if (index === -1) {
        this.checkList.push(v);
      } else {
        this.checkList.splice(index, 1);
      }
    //   console.log(this.checkList);
      this.$emit("getCheckList", {
        checkList: this.checkList,
        type: this.$props.hotelConditionsKey
      });
    }
  }
};
</script>

<style>
</style>
