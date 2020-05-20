<template>
  <div class="container">
    <el-card class="box-card">
      <div slot="header" class="clearfix">
        <span style="float: left;">账号管理</span>
        <el-button style="float: right;" type="primary" @click="handleAdd()">新增</el-button>
      </div>
      <el-table :data="tableData" style="width: 100%">
        <el-table-column prop="userName" label="用户名" width="180"></el-table-column>
        <el-table-column prop="password" label="密码" width="180"></el-table-column>
        <el-table-column fixed="right" label="操作" width="100">
          <template slot-scope="scope">
            <el-button type="primary" @click="handleEdit(scope.row)" size="small">编辑</el-button>
          </template>
        </el-table-column>
      </el-table>
    </el-card>
    <modal :visible="visible"/>
  </div>
</template>

<script>
import Modal from '../components/Modal';
export default {
  name: "Home",
  components: {
    Modal
  },
  created() {
    this.$http.get("api/v1/users").then(({ data }) => {
      if (data.success) {
        this.tableData = data.data;
      }
    });
  },
  data() {
    return {
      visible: false,
      tableData: []
    };
  },
  methods: {
    handleAdd() {
      this.visible = true;
    }
  }
};
</script>
<style lang="less" dscoped>
.container {
  max-width: 800px;
  margin: auto;
  .text {
    font-size: 14px;
  }

  .item {
    margin-bottom: 18px;
  }

  .clearfix:before,
  .clearfix:after {
    display: table;
    content: "";
  }
  .clearfix:after {
    clear: both;
  }

  .box-card {
    width: 480px;
  }
}
</style>