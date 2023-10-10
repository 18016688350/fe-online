<template>
  <el-tree :data="result.list" @node-click="nodeClick">
    <template #default="{ node, data }">
      <el-icon>
        <Service />
      </el-icon>{{ node.label }}
    </template>
  </el-tree>
</template>

<script lang="ts" setup>
import { ref, reactive } from 'vue'


import userApi from '../api/user'

const result = reactive({
  list: [],
});

userApi.query({}).then((users) => {
  users.forEach(user => {
    user.label = user.name
  });
  result.list = users;
})
const emit = defineEmits(['nodeResult'])
const nodeClick = (node) => {
  emit('nodeResult', node)
}
</script>