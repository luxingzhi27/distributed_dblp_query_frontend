<script setup>
import { ref,computed } from 'vue'

const author = ref('')
const lowerYear = ref(2020)
const upperYear = ref(2023)

const result = ref(16)

const xmlQueryTime = ref(30)
const hashQueryTime = ref(15)

const faster= computed(() => {
  return 100*(xmlQueryTime.value -hashQueryTime.value)/xmlQueryTime.value
})

const query = () => {
  console.log(author.value)
  console.log(lowerYear.value)
  console.log(upperYear.value)
}

</script>

<template>
    <div class="col container">
      <div class="query-header">
        <h1>Distributed dblp dataset query</h1>
        <el-button type="success" @click="query" style="margin-right: 10px">Query</el-button>
      </div>
      <div class="row" style="margin-bottom: 10px">
        <span style="margin-right: 10px;width: fit-content;font-weight: bold;" class="label-text">
          author
        </span>
        <el-input  class="mx-2" v-model="author" placeholder="Type author's name" :prefix-icon="Search"/>
      </div>
      <div style="display: flex; align-items: center">
        <div class="row year-input" style="margin-right: 2px">
          <span style="margin-right: 10px;width: fit-content;font-weight: bold" class="label-text">
            lower year
          </span>
            <el-input-number   v-model="lowerYear" :min="0" :max="upperYear"   placeholder="Lower bound"/>
        </div>

        <div class="row year-input" style="margin-left:20px">
          <span style="margin-right: 10px;width: fit-content;font-weight: bold" class="label-text">
            upper year
          </span>
          <el-input-number   v-model="upperYear" :min="lowerYear" :max="2023"  placeholder="Upper bound"/>
        </div>
      </div>
      <h1 style="font-size: 25px">Query Result</h1>
      <el-card>
        <el-row>
          <div style="display: flex;align-items: center">
            <span style="font-weight: bold;">
              总共查询到
            </span>
            <span style="font-weight: bold;font-size: 50px;color: crimson;margin-right: 4px;margin-left: 4px">{{result}}</span>
            <span style="font-weight: bold">条数据</span>
          </div>
        </el-row>

        <el-row>
          <div style="display: flex;align-items: center">
            <span style="font-weight: bold;">
              xml查询耗时
            </span>
            <span style="font-weight: bold;font-size: 50px;color:deepskyblue;margin-right: 4px;margin-left: 4px">{{xmlQueryTime}}</span>
            <span style="font-weight: bold">秒, </span>
            <span style="font-weight: bold;">
              哈希表查询耗时
            </span>
            <span style="font-weight: bold;font-size: 50px;color:firebrick;margin-right: 4px;margin-left: 4px">{{hashQueryTime}}</span>
            <span style="font-weight: bold">秒</span>
          </div>
        </el-row>
        <el-row>
          <div style="display: flex;align-items: center">
            <span style="font-weight: bold">哈希表快</span>
            <span class="percentage" style="font-weight: bold;font-size: 50px;color: limegreen;margin-left: 4px;margin-right: 4px">{{faster}}</span>
          </div>
        </el-row>

      </el-card>
    </div>
</template>

<style scoped>

.container{
  width: 80%;
}

.percentage::after{
  content: '%';
  font-size: 50px;
  font-weight: bold;
  color:limegreen;
}

el-card{
  font-size: 20px;
}

.query-header{
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.col{
  display: flex;
  flex-direction: column;
  justify-content: center;
}

.year-input{
  margin-bottom: 10px;
  margin-top: 10px;
}


.label-text{
  color: whitesmoke;
  font-size: 18px;
}

.row{
  display: flex;
  flex-direction: row;
  align-items: center;
}
</style>