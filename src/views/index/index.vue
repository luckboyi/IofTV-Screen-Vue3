<!--
 * @Author: zhengyi yi.zheng@yunzhihulian.cn
 * @Date: 2024-04-18 15:26:00
 * @LastEditors: zhengyi yi.zheng@yunzhihulian.cn
 * @LastEditTime: 2024-04-19 18:22:01
 * @FilePath: \IofTV-Screen-Vue3\src\views\index\index.vue
 * @Description: 这是默认设置,请设置`customMade`, 打开koroFileHeader查看配置 进行设置: https://github.com/OBKoro1/koro1FileHeader/wiki/%E9%85%8D%E7%BD%AE
-->
<script setup lang="ts">
import ItemWrap from "@/components/item-wrap";
import LeftTop from "./left-top.vue";
import LeftCenter from "./left-center.vue";
import LeftCenter2 from "./left-center2.vue";
import LeftBottom from "./left-bottom.vue";
import CenterMap from "./center-map.vue";
import CenterBottom from "./center-bottom.vue";
import RightTop from "./right-top.vue";
import RightCenter from "./right-center.vue";
import RightBottom from "./right-bottom.vue";
import RightTop2 from './right-top2.vue'
</script>

<template>
  <div class="index-box">
    <div class="contetn_left">
      <!-- <div class="pagetab">
        <div class="item">实时监测</div>
        <div class="item">统计分析</div>
      </div> -->
      <ItemWrap class="contetn_left-top contetn_lr-item" title="设备总览">
        <LeftTop />
      </ItemWrap>
      <ItemWrap class="contetn_left-center contetn_lr-item" title="用户总览">
        <LeftCenter />
      </ItemWrap>
      <ItemWrap
        class="contetn_left-bottom contetn_lr-item contetn_lr-item5"
        title="设备提醒"
        style="padding: 0 10px 16px 10px"
      >
        <LeftBottom />
      </ItemWrap>
    </div>
    <div class="contetn_center">
      <CenterMap class="contetn_center_top" title="设备分布图" />
      <ItemWrap class="contetn_center-bottom" title="异常报警提醒">
        <!-- <CenterBottom /> -->
        <RightBottom />
      </ItemWrap>
    </div>
    <div class="contetn_right">
      <!-- <ItemWrap class="contetn_left-bottom contetn_lr-item" title="工单处理统计">
        <RightTop/>
      </ItemWrap> -->
      <ItemWrap class="contetn_left-bottom contetn_lr-item contetn_lr-item1" title="工单处理统计">
        <RightTop2/>
      </ItemWrap>
      <ItemWrap
        class="contetn_left-bottom contetn_lr-item contetn_lr-item2"
        title="今日异常统计"
        style="padding: 0 10px 16px 10px"
      >
        <RightCenter />
      </ItemWrap>
      <ItemWrap
        class="contetn_left-bottom contetn_lr-item contetn_lr-item2"
        title="今日工单处理统计"
        style="padding: 0 10px 16px 10px"
      >
        <LeftCenter2 />
      </ItemWrap>
    </div>
  </div>
</template>

<style scoped lang="scss">
.index-box {
  width: 100%;
  display: flex;
  min-height: calc(100% - 64px);
  justify-content: space-between;
}
//左边 右边 结构一样
.contetn_left,
.contetn_right {
  display: flex;
  flex-direction: column;
  justify-content: space-around;
  position: relative;
  width: 540px;
  box-sizing: border-box;
  flex-shrink: 0;
}
.contetn_center {
  flex: 1;
  margin: 0 10px;
  display: flex;
  flex-direction: column;
  justify-content: space-around;
  .contetn_center-bottom {
    height: 336px;
  }
}

.contetn_lr-item {
  height: 310px;
}
.contetn_lr-item2{
  height: 330px;
}
// .contetn_lr-item2{
//   height: 250px !important;
// }
// .contetn_lr-item3{
//   height: 330px !important;
// }
.contetn_lr-item5{
  height: 346px !important;
}
</style>
