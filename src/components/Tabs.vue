<template>
  <div class="common-layout">
    <el-container>
      <el-header>
        <el-tabs v-model="activeName" class="demo-tabs" @tab-click="handleClick">
          <el-tab-pane label="成员管理" name="member"></el-tab-pane>
          <el-tab-pane label="团队管理" name="team"></el-tab-pane>
          <el-tab-pane label="职位维护" name="position"></el-tab-pane>
        </el-tabs>
      </el-header>
      <el-container>
        <el-aside width="350px" class="borderF6" style="padding: 0 0 20px 0px; ">
          <el-row class="h40" style="border-bottom:1px solid #F6F6F6;;">
            <el-col :span="20" class="paddingLt20">部门</el-col>
            <el-col :span="4">+</el-col>
          </el-row>
          <Tree @nodeResult="nodeResult" />
        </el-aside>
        <el-main class="borderF6">
          <div class="h40 paddingLt20" style="border-bottom: 1px solid #F6F6F6;">厦门嗨行旅游 / 技术部</div>
          <el-row class="h40 paddingLt20">
            <el-col :span="6">
              <el-input style="width:100%" clearable class="w-50 m-2 " placeholder="输入关键字">
                <template #suffix>
                  <!-- <el-icon  class="iconfont link-search mr-t" /> --> ∨
                </template>
                <template #prefix>
                  <!-- <el-icon  class="iconfont link-search mr-t" /> --> O
                </template>
              </el-input>
            </el-col>
            <div style="color:#F6F6F6">|</div>

            <div style="margin:0 20px 0 20px;">登录状态 ∨</div>
            <div>1个成员</div>
          </el-row>
          <div class="paddingLt20">
            <el-table ref="multipleTableRef" border :data="result.list" style="width: 100%">
              <el-table-column type="selection" width="55" />
              <el-table-column property="name" sortable label="姓名" />
              <el-table-column property="id" sortable label="用户名" />
            </el-table>
          </div>
        </el-main>
      </el-container>
    </el-container>
  </div>
</template>

<script lang="ts" setup>
import Tree from './Tree.vue'
import orgApi from '../api/org'
import { ref, reactive } from 'vue'
import type { TabsPaneContext } from 'element-plus'
const activeName = ref('member')

const handleClick = (tab: TabsPaneContext, event: Event) => { }


const result = reactive({
  list: [],
});
const getOrg = () => {
  orgApi.query('1').then((users) => {
    users.forEach(user => {
      user.label = user.name
    });
    result.list = users;
    console.log(result.list)
  })
}
getOrg()

const nodeResult = () => {
  getOrg()

}


</script>

<style scoped>
.read-the-docs {
  color: #888;
}

::v-deep .el-tree-node__content {
  height: 36px;
  line-height: 36px;
}

::v-deep .el-main {
  padding: 0px !important;
}

::v-deep .el-input .el-input__wrapper {
  background: none;
  box-shadow: none;
}

.h40 {
  height: 40px;
  line-height: 40px
}

.borderF6 {
  border: 1px solid #F6F6F6
}

.paddingLt20 {
  padding-left: 20px;
}</style>

