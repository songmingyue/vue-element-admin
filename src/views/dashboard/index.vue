<template>
  <div class="dashboard-container">
    <div class="table-watch">
      <el-table
        :data="tableData"
        border
        style="width: 100%"
      >
        <el-table-column
          prop="kaNames"
          label="卡片"
        />
        <el-table-column
          prop="StockAmount"
          label="数量"
        />
        <el-table-column
          prop="rate"
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
        const kaName = {
          '101': '浪',
          '102': '漫',
          '103': '波',
          '104': '比'
        }
        if (res && res.data && res.data.Stock) {
          const rates = res.data.MainPool
          res.data.Stock.map((item, index) => {
            // 数据处理，把code变为
            item.kaNames = item.StockType === 2 ? `必中卡(${kaName[item.StockCode]})` : kaName[item.StockCode]
            item.rate = index > 3 ? '' : rates[index].rate
          })
        }
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
