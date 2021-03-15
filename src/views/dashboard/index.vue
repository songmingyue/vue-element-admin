<template>
  <div class="dashboard-container">
    <div class="table-watch">
      <el-table
        :data="tableData"
        border
        style="width: 100%"
      >
        <el-table-column
          prop="StockCode"
          label="卡片"
        />
        <el-table-column
          prop="StockAmount"
          label="数量"
        />
        <el-table-column
          prop="StockType"
          label="概率"
        />
      </el-table>
    </div>
  </div>
</template>
<script>
import axios from 'axios'
export default {
  name: 'Dashboard',
  data() {
    return {
      tableData: []
    }
  },
  computed: {},
  created() {
    this.getNum()
  },
  methods: {
    getNum() {
      axios.post('https://apipro.playinjoy.com/legion/bstock').then(res => {
        console.log(res.data.Stock)
        this.tableData = res.data.Stock
      })
    }
  }
}
</script>
<style scoped>
.table-watch {
  width: 80%;
}
</style>
