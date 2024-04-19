<template>
  <div class="totalCon">
    <el-row :gutter="10">
      <el-col :span="8">
        <div class="inCon">
          <h3>今年已累计处理异常</h3>
          <p><b>152,351,255</b>条</p>
        </div>
      </el-col>
      <el-col :span="8">
        <div class="inCon">
          <h3>本周处理异常</h3>
          <p><b>6,598,426</b>条</p>
        </div>
      </el-col>
      <el-col :span="8">
        <div class="inCon">
          <h3>今日处理异常</h3>
          <p><b>65,231</b>条</p>
        </div>
      </el-col>
    </el-row>
    <el-row :gutter="10" class="marginTop10">
      <el-col :span="8">
        <div class="inCon">
          <h3>今年已累计工单</h3>
          <p><b>22,222</b>条</p>
        </div>
      </el-col>
      <el-col :span="8">
        <div class="inCon">
          <h3>本周处理工单</h3>
          <p><b>626</b>条</p>
        </div>
      </el-col>
      <el-col :span="8">
        <div class="inCon">
          <h3>今日处理工单</h3>
          <p><b>21</b>条</p>
        </div>
      </el-col>
    </el-row>
  </div>
</template>
<style lang="scss" scoped>
.totalCon {
    padding: 20px 0;
  .el-col {
    .inCon {
      background: rgb(32 53 90 / 50%);
      border-radius: 10px;
      padding: 10px 6px;
      box-sizing: border-box;
      h3{
        line-height: 40px;
        color: #1890ff;
        font-weight: 700;

      }
      b{
        color: aquamarine;
        margin-right: 10px;
      }
    }
  }
  .marginTop10{
    margin-top: 20px;
  }
}
</style>
