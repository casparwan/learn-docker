<template>
  <el-dialog title="收货地址" :visible.sync="visible">
    <el-form :model="form">
      <el-form-item label="用户名" :label-width="formLabelWidth">
        <el-input v-model="form.userName" autocomplete="off"></el-input>
      </el-form-item>
      <el-form-item label="密码" :label-width="formLabelWidth">
        <el-input v-model="form.password" autocomplete="off"></el-input>
      </el-form-item>
    </el-form>
    <div slot="footer" class="dialog-footer">
      <el-button @click="visible = false">取 消</el-button>
      <el-button type="primary" @click="save()">确 定</el-button>
    </div>
  </el-dialog>
</template>

<script>
export default {
  props: {
    visible: Boolean
  },
  data() {
    return {
      form: {
        userName: "",
        password: ""
      },
      formLabelWidth: "120px"
    };
  },
  methods: {
    save() {
      const body = this.form;
    //   this.axios.post("/api/v1/users", body).then(({ data }) => {
    //     if (data.success) {
    //       this.visible = false;
    //     }
    //   });
      fetch("/api/v1/users", {
        method: "POST", // or 'PUT'
        body: JSON.stringify(body), // data can be `string` or {object}!
        headers: new Headers({
          "Content-Type": "application/json"
        })
      })
        .then(res => res.json())
        .catch(error => console.error("Error:", error))
        .then(response => console.log("Success:", response));
    }
  }
};
</script>
<style lang="less" dscoped>
</style>