<template>
  <el-row :gutter="20">
    <h3>天线状态</h3>
    <el-divider />
    <el-col :span="24">
      <el-table v-loading="loading" :data="tableData" border style="width: 100%">
        <el-table-column prop="project" label="项目" />
        <el-table-column prop="status" label="当前状态" />
      </el-table>
    </el-col>
  </el-row>
</template>

<script>
import { getAntennaStatus } from '@/api/dashboard/antennaStatus'
export default {
  name: 'AntennaStatus',
  data() {
    return {
      tableData: [],
      loading: false
    }
  },
  created() {
    this.getStatus()
  },
  methods: {
    getStatus() {
      this.loading = true
      getAntennaStatus().then(response => {
        this.tableData = response.data.items
      })
      setTimeout(() => {
        this.loading = false
      }, 1.5 * 1000)
    }
  }
}
</script>
