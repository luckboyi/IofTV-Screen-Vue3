<!--
 * @Author: zhengyi yi.zheng@yunzhihulian.cn
 * @Date: 2024-04-18 15:26:00
 * @LastEditors: zhengyi yi.zheng@yunzhihulian.cn
 * @LastEditTime: 2024-04-19 18:10:24
 * @FilePath: \IofTV-Screen-Vue3\src\views\index\right-center.vue
 * @Description: 这是默认设置,请设置`customMade`, 打开koroFileHeader查看配置 进行设置: https://github.com/OBKoro1/koro1FileHeader/wiki/%E9%85%8D%E7%BD%AE
-->
<script setup lang="ts">
import { ref, reactive } from "vue";
import CapsuleChart from "@/components/datav/capsule-chart";
import { ranking } from "@/api";
import { ElMessage } from "element-plus";
const props = defineProps<{
    type:any;
  }>();
const config = ref({
  showValue: true,
  unit: "次",
});
const data = ref([]);
const getData = () => {
  ranking()
    .then((res) => {
      if (res.success) {
        console.log(res.data)
        data.value = res.data;
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
getData();
</script>

<template>
  <div class="right_bottom">
    <CapsuleChart :config="config" style="width: 100%; height: 260px" :data="data" />
  </div>
</template>

<style scoped lang="scss">
.right_bottom {
  box-sizing: border-box;
  padding: 0 16px;
}
</style>
