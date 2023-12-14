<script setup>
import Query from '@/components/Query.vue'
</script>

<template>
  <el-row>
    <el-col :span="3" />
    <el-col :span="18">
      <div class="main">
        <Query />
      </div>
    </el-col>
    <el-col :span="3"/>
  </el-row>

</template>

<style scoped>
.main{
  display:flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}
</style>
