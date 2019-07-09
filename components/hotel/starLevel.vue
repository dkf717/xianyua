<template>
  <span :title="level + '星级'">
    <i v-for="v in level" class="iconfont iconhuangguan" :key="v" />
  </span>
</template>

<script>
export default {
  props: ["level"]
};
</script>

<style>
</style>
