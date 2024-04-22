<script setup lang="ts">
import { rightBottom } from "@/api";
import SeamlessScroll from "@/components/seamless-scroll";
import { computed, onMounted, reactive } from "vue";
import { useSettingStore } from "@/stores";
import { storeToRefs } from "pinia";
import EmptyCom from "@/components/empty-com";
import { ElMessage } from "element-plus";

const settingStore = useSettingStore();
const { defaultOption, indexConfig } = storeToRefs(settingStore);
const state = reactive<any>({
  list: [],
  defaultOption: {
    ...defaultOption.value,
    singleHeight: 266,
    limitScrollNum: 3,
    // step:3
  },
  scroll: true,
});

const getData = () => {
  rightBottom({ limitNum: 20 })
    .then((res) => {
      console.log("右下", res);
      const array = ["特别紧急", "紧急", "高", "中", "低"];
      const alertdetail = [
        "温度过高",
        "CPU使用率超高",
        "内存使用率过高",
        "内存使用过高",
        "发生蓝屏",
        "磁盘Io异常",
        "网卡异常",
        "网速异常",
      ];
      // 从数组中随机选择一个元素
      if (res.success) {
        res.data.list.forEach((element: any) => {
          const randomElement = array[Math.floor(Math.random() * array.length)];
          const randomDeail =
            alertdetail[Math.floor(Math.random() * array.length)];
          element.alertdetail = randomDeail;
          element.WarningTxt = randomElement;
          
        });
        state.list = res.data.list;
      } else {
        ElMessage({
          message: res.msg,
          type: "warning",
        });
      }
    })
    .catch((err) => {
      ElMessage.error(err);
    });
};

const comName = computed(() => {
  if (indexConfig.value.rightBottomSwiper) {
    return SeamlessScroll;
  } else {
    return EmptyCom;
  }
});
function montionFilter(val: any) {
  // console.log(val);
  return val ? Number(val).toFixed(2) : "--";
}
const handleAddress = (item: any) => {
  return `${item.provinceName}/${item.cityName}/${item.countyName}`;
};
onMounted(() => {
  getData();
});
</script>

<template>
  <div
    class="right_bottom_wrap beautify-scroll-def"
    :class="{ 'overflow-y-auto': !indexConfig.rightBottomSwiper }"
  >
    <component
      :is="comName"
      :list="state.list"
      v-model="state.scroll"
      :singleHeight="state.defaultOption.singleHeight"
      :step="state.defaultOption.step"
      :limitScrollNum="state.defaultOption.limitScrollNum"
      :hover="state.defaultOption.hover"
      :singleWaitTime="state.defaultOption.singleWaitTime"
      :wheel="state.defaultOption.wheel"
    >
      <ul class="right_bottom">
        <li class="right_center_item" v-for="(item, i) in state.list" :key="i">
          <span class="orderNum">{{ i + 1 }}</span>
          <div class="inner_right">
            <div class="dibu"></div>
            <div class="flex">
              <div class="info">
                <span class="labels">设备ID：</span>
                <span class="text-content zhuyao"> {{ item.gatewayno }}</span>
              </div>
              <div class="info">
                <span class="labels">型号：</span>
                <span class="text-content"> {{ item.terminalno }}</span>
              </div>
              <div class="info">
                <span class="labels">告警值：</span>
                <span class="text-content warning">
                  {{ montionFilter(item.alertvalue) }}</span
                >
              </div>
            </div>

            <div class="flex">
              <div class="info">
                <span class="labels shrink-0"> 地址：</span>
                <span
                  class="truncate ciyao"
                  style="font-size: 12px; width: 220px"
                  :title="handleAddress(item)"
                >
                  {{ handleAddress(item) }}</span
                >
              </div>
              <div class="info time shrink-0">
                <span class="labels">时间：</span>
                <span class="text-content" style="font-size: 12px">
                  {{ item.createtime }}</span
                >
              </div>
            </div>
            <div class="flex">
              <div class="info">
                <span class="labels">报警内容：</span>
                <span
                  class="text-content ciyao"
                  :class="{ warning: item.alertdetail }"
                >
                  {{ item.alertdetail || "无" }}</span
                >
              </div>
              <div class="info time shrink-0">
                <span class="labels">报警级别：</span>
                <span class="text-content" style="font-size: 12px">
                  <b class="error1" v-if="item.WarningTxt == '特别紧急'">{{
                    item.WarningTxt
                  }}</b>
                  <b class="error2" v-if="item.WarningTxt == '紧急'">{{
                    item.WarningTxt
                  }}</b>
                  <b class="error3" v-if="item.WarningTxt == '高'">{{
                    item.WarningTxt
                  }}</b>
                  <b class="error4" v-if="item.WarningTxt == '中'">{{
                    item.WarningTxt
                  }}</b>
                  <b class="error5" v-if="item.WarningTxt == '低'">{{
                    item.WarningTxt
                  }}</b>
                </span>
              </div>
            </div>
          </div>
        </li>
      </ul>
    </component>
  </div>
</template>

<style scoped lang="scss">
.right_bottom {
  width: 100%;
  height: 100%;
  .flex {
    display: inline-block;
  }
  .right_center_item {
    display: flex;
    align-items: center;
    justify-content: center;
    height: auto;
    padding: 10px;
    font-size: 14px;
    color: #fff;

    .orderNum {
      margin: 0 20px 0 -20px;
    }

    .inner_right {
      position: relative;
      height: 100%;
      width: calc(100% - 30px);
      flex-shrink: 0;
      line-height: 1.5;

      .dibu {
        position: absolute;
        height: 2px;
        width: 104%;
        background-image: url("@/assets/img/zuo_xuxian.png");
        bottom: -12px;
        left: -2%;
        background-size: cover;
      }
    }

    .info {
      margin-right: 10px;
      display: flex;
      align-items: center;

      .labels {
        flex-shrink: 0;
        font-size: 12px;
        color: rgba(255, 255, 255, 0.6);
      }

      .zhuyao {
        color: $primary-color;
        font-size: 15px;
      }

      .ciyao {
        color: rgba(255, 255, 255, 0.8);
      }

      .warning {
        color: #e6a23c;
        font-size: 15px;
      }
    }
  }
}

.right_bottom_wrap {
  overflow: hidden;
  width: 100%;
  height: 252px;
}

.overflow-y-auto {
  overflow-y: auto;
}
.error1 {
  color: #fd1d1d;
  font-size: 16px !important;
  font-weight: 700;
}
.error2 {
  color: #e6503c;
  font-size: 16px !important;
  font-weight: 700;
}
.error3 {
  color: #d83ce6;
  font-size: 16px !important;
  font-weight: 700;
}
.error4 {
  color: #e6a23c;
  font-size: 16px !important;
  font-weight: 700;
}
.error5 {
  color: #3ce645;
  font-size: 16px !important;
  font-weight: 700;
}
</style>
