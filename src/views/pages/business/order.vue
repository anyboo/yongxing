<template>
  <div>
    <div class="Vheader">
      <!-- 搜索框 -->
      <SearchBox :onsearch="search"></SearchBox>
      <!-- 按钮组 -->
      <div class="btnGroup">
        <el-button type="success" icon="plus" @click="openModel(1)">添加</el-button>
        <el-button type="info" icon="edit" @click="openModel(0)">编辑</el-button>
        <el-button type="danger" icon="delete"  @click="delMsg()">删除</el-button>
      </div>
    </div>

    <!-- 表格 -->
    <div>
      <el-table highlight-current-row :data="tableData" border style="width: 100%" ref="table" :default-sort="{prop: 'date', order: 'descending'}"
        @current-change="tableCurrentChange">
        <el-table-column type="selection" width="55">
        </el-table-column>
        <el-table-column prop="orderId" label="单号" >
        </el-table-column>
        <el-table-column prop="orderName" label="接单员" >
        </el-table-column>
        <el-table-column prop="orderNumber" label="联系方式">
        </el-table-column>
        <el-table-column prop="servicePosition" label="维修位置">
        </el-table-column>
        <el-table-column prop="serviceContent" label="内容">
        </el-table-column>
        <el-table-column prop="materialCost" label="材料费">
        </el-table-column>
        <el-table-column prop="serviceCost" label="维修费">
        </el-table-column>
        <el-table-column prop="serviceTotal" label="合计">
        </el-table-column>
        <el-table-column prop="isOrder" label="是否接单" width="120">
        </el-table-column>
        
      </el-table>
    </div>

    <!-- 分页 -->
    <PageBar :pageData="pageData" :getData="getInfo" ></PageBar>
    <!-- 弹出框 -->
    <el-dialog :title="modelTitle" :visible.sync="modelShow">
      <el-form :model="form" label-width="80px" :rules="rules" ref="ruleForm">
        <el-form-item label="部门" prop="department">
          <el-input v-model="form.department"></el-input>
        </el-form-item>
        <el-form-item label="姓名" prop="employee_name">
          <el-input v-model="form.employee_name"></el-input>
        </el-form-item>
        <el-form-item label="联系方式" prop="telephone_number">
          <el-input v-model="form.telephone_number"></el-input>
        </el-form-item>
         <el-form-item label="职务" prop="position" >
          <el-input v-model="form.position"></el-input>
        </el-form-item>
        <el-form-item label="openId">
          <el-input v-model="form.wxopen_id"></el-input>
        </el-form-item>
        <el-form-item label="备注">
          <el-input v-model="form.note"></el-input>
        </el-form-item>

      </el-form>
      <div slot="footer" class="dialog-footer">
        <el-button @click="modelShow = false">取 消</el-button>
        <el-button type="primary" @click="okModel">确 定</el-button>
      </div>
    </el-dialog>


  </div>
</template>

<script>
import mixin from "@/minix/index.js";
import * as api from "@/api/serviceReceiving";
export default {
  name: "order",
  mixins: [mixin],
  mounted() {
    this.getInfo();
  },
  data() {
    return {
      form: {
        department: "",
        employee_name: "",
        telephone_number: "",
        wxopen_id: "",
        note: "",
        position: ""
      },

      
    };
  },

  methods: {


    //莫谈框点击确定
    okModel() {
      this.$refs["ruleForm"].validate(valid => {
        if (valid) {
          console.log("submit!");
          if (this.isAdd) {
            //添加操作
            
          } else {
            //编辑操作
           
          }
         
        } else {
          console.log("error submit!!");
          return false;
        }
      });
    },

    //获取分页数据
    getInfo() {
      api
        .getBusinessReceive(this.pageData.page - 1, this.pageData.pageSize)
        .then(res => {
          console.log(res);
          this.tableData = res.data;
          this.pageData.total = res.count;
        });
    },

     //删除数据
    delItem() {
      if (this.checkId) {
        
      }
    },

    //点击搜索按钮
    search(i) {
      console.log(i);
    }
  }
};
</script>

<style scoped lang='scss'>

</style>
