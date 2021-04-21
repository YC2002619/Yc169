<template>
  <div class="div_d">
    <div class="div_d1">
      <div class="block">
        <span class="demonstration">卫生检查日期</span>
        <el-date-picker
          v-model="qk.checkDate"
          type="date"
          placeholder="选择日期"
          value-format="yyyy-MM-dd"
          format="yyyy-MM-dd"
        ></el-date-picker>

        <el-button type="primary" icon="el-icon-search" @click="Chax" class="el_button_1">查询</el-button>
        <el-button plain icon="el-icon-refresh" @click="qingk">重置</el-button>
      </div>
    </div>

    <div class="div_d3">
      <el-row class="el_row_1">
        <el-button type="primary" icon="el-icon-plus" @click="Xinz = true">新增</el-button>
        <el-button type="success" icon="el-icon-edit">修改</el-button>
        <el-button type="danger" icon="el-icon-delete">删除</el-button>
      </el-row>

      <!-- 添加 -->
      <el-dialog title="宿舍添加信息" :visible.sync="Xinz">
        <el-form
          :model="ruleForm"
          :rules="rules"
          label-width="100px"
          class="demo-ruleForm"
        >
          <div class="div_d6">
            <div class="block">
              <span class="demonstration">卫生检查日期</span>
              <el-date-picker
                v-model="ruleForm.checkDate"
                type="date"
                placeholder="选择日期"
                value-format="yyyy-MM-dd"
                format="yyyy-MM-dd"
                :label="xs.checkDate"
              ></el-date-picker>
            </div>

            <div class="demo-input-suffix sb1">
              宿舍栋号
              <el-select v-model="ruleForm.buildingNo" placeholder="请输入宿舍栋号">
                <el-option
                  v-for="(item1, key1) in list1"
                  :key="key1"
                  :value="item1.dictValue"
                >{{item1.dictLabel}}</el-option>
              </el-select>
            </div>

            <div class="demo-input-suffix sb1">
              宿舍楼层
              <el-select v-model="ruleForm.storey" placeholder="请输入宿舍楼层">
                <el-option
                  v-for="(item2, key2) in list2"
                  :key="key2"
                  :value="item2.dictValue"
                >{{item2.dictLabel}}</el-option>
              </el-select>
            </div>

            <div class="demo-input-suffix sb1" @click="xiala3">
              宿舍号
              <el-select v-model="ruleForm.dormitoryNo" placeholder="请输入宿舍号">
                <el-option
                  v-for="(item3, key3) in list3"
                  :key="key3"
                  :value="item3.dormitoryNo"
                >{{item3.dormitoryNo}}</el-option>
              </el-select>
            </div>

            <div class="demo-input-suffix sb1">
              卫生项
              <el-select v-model="ruleForm.deductOption" multiple placeholder="请选择">
                <el-option
                  v-for="(item4, key4) in list4"
                  :key="key4"
                  :label="item4.deductOption"
                  :value="item4.id"
                ></el-option>
              </el-select>
            </div>

            <div class="demo-input-suffix sb1">
              属性方式：
              <el-input
                type="textarea"
                :rows="2"
                placeholder="请输入内容"
                v-model="ruleForm.remark"
                class="lm"
              ></el-input>
            </div>
          </div>
        </el-form>
        <div class="demo-input-suffix div_d8">
          <span slot="footer" class="dialog-footer">
            <el-button @click="Xinz = false">取 消</el-button>
            <el-button type="primary" @click="submitForm">确 定</el-button>
          </span>
        </div>
      </el-dialog>

      <!-- 修改 -->
      <el-dialog title="宿舍修改信息" :visible.sync="dialogFormVisible2">
        <el-form
          :model="ruleForm2"
          :rules="rules"
          label-width="100px"
          class="demo-ruleForm"
        >
          <div class="div_d6">
            <div class="block">
              <span class="demonstration">卫生检查日期</span>
              <el-date-picker
                v-model="ruleForm2.checkDate"
                type="date"
                placeholder="选择日期"
                value-format="yyyy-MM-dd"
                format="yyyy-MM-dd"
              ></el-date-picker>
            </div>

             <div class="demo-input-suffix sb1">
              宿舍栋号
              <el-select v-model="ruleForm2.buildingNo" placeholder="请输入宿舍栋号">
                <el-option
                  v-for="(item1, key1) in list1"
                  :key="key1"
                  :value="item1.dictValue"
                >{{item1.dictLabel}}</el-option>
              </el-select>
            </div>

            <div class="demo-input-suffix sb1">
              宿舍楼层
              <el-select v-model="ruleForm2.storey" placeholder="请输入宿舍楼层">
                <el-option
                  v-for="(item2, key2) in list2"
                  :key="key2"
                  :value="item2.dictValue"
                >{{item2.dictLabel}}</el-option>
              </el-select>
            </div>

            <div class="demo-input-suffix sb1" @click="xiala3">
              宿舍号
              <el-select v-model="ruleForm2.dormitoryNo" placeholder="请输入宿舍号">
                <el-option
                  v-for="(item3, key3) in list3"
                  :key="key3"
                  :value="item3.dormitoryNo"
                >{{item3.dormitoryNo}}</el-option>
              </el-select>
            </div>

            <div class="demo-input-suffix sb1">
              卫生项
              <el-select v-model="ruleForm2.deductOption" multiple placeholder="请选择">
                <el-option
                  v-for="(item4, key4) in list4"
                  :key="key4"
                  :label="item4.deductOption"
                  :value="item4.id"
                ></el-option>
              </el-select>
            </div>

            <div class="demo-input-suffix sb1">
              属性方式：
              <el-input
                type="textarea"
                :rows="2"
                placeholder="请输入内容"
                v-model="ruleForm2.remark"
                class="lm"
              ></el-input>
            </div>
          </div>
        </el-form>
        <div class="demo-input-suffix div_d8">
          <span slot="footer" class="dialog-footer">
            <el-button @click="dialogFormVisible2 = false">取 消</el-button>
            <el-button type="primary" @click="Xiuggqr">确 定</el-button>
          </span>
        </div>
      </el-dialog>

      <div class="div_d4">
        <el-table ref="multipleTable" :data="jb" tooltip-effect="dark" style="width: 100%">
          <el-table-column type="selection" width="55"></el-table-column>
          <el-table-column label="序号" width="120">
            <template slot-scope="scope">{{ scope.row.id }}</template>
          </el-table-column>
          <el-table-column prop="checkDate" label="卫生检查日期"></el-table-column>
          <el-table-column prop="buildingNo" label="宿舍栋号"></el-table-column>
          <el-table-column prop="storey" label="楼层"></el-table-column>
          <el-table-column prop="dormitoryNo" label="宿舍号"></el-table-column>
          <el-table-column prop="deductIds" label="卫生扣分项"></el-table-column>
          <el-table-column prop="totalPdeduct" label="总扣分"></el-table-column>
          <el-table-column prop="totalScore" label="总得分"></el-table-column>
          <el-table-column prop="modifyTime" label="创建时间"></el-table-column>
          <el-table-column label="操作">
            <template slot-scope="scope">
              <el-button type="success" icon="el-icon-edit" circle @click="Xiug(scope.row.id)"></el-button>
              <el-button type="danger" icon="el-icon-delete" circle @click="Delete(scope.row.id)"></el-button>
            </template>
          </el-table-column>
        </el-table>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      textarea: "",
      list1: [],
      list2: [],
      list3: [],
      list4: [],
      jb: [],
      rules: {
        name: [
          { required: true, message: "班级名称不能为空", trigger: "blur" }
        ],
        region: [
          { required: true, message: "班主任不能为空", trigger: "change" }
        ]
      },
      Xinz: false,
      dialogFormVisible2: false,
      ruleForm: {
        checkDate: "",
        buildingNo: "",
        storey: "",
        dormitoryNo: "",
        deductOption: "",
        remark: ""
      },
      ruleForm2: {
        checkDate: "",
        buildingNo: "",
        storey: "",
        dormitoryNo: "",
        deductOption: "",
        remark: ""
      },
      pageNum: 1,
      pageSize: 100,

      qk: {
        checkDate: ""
      },
      xs: {
        checkDate: "",
        buildingNo: []
      }
    };
  },
  mounted() {
    this.xiala1();
    this.xiala2();
    this.xiala4();
    this.xians();
  },
  methods: {
    xiala1() {
      var that = this;
      that
        .axios({
          url:
            "http://122.112.253.28:8095/prod-api/sys/dict/detail/dictType/sys_building",
          method: "GET",
          headers: {
            Authorization: window.sessionStorage.token
          }
        })
        .then(response => {
          that.list1 = response.data.data;
        });
    },

    xiala2() {
      var that = this;
      that
        .axios({
          url:
            "http://122.112.253.28:8095/prod-api/sys/dict/detail/dictType/sys_storey",
          method: "GET",
          headers: {
            Authorization: window.sessionStorage.token
          }
        })
        .then(response => {
          that.list2 = response.data.data;
        });
    },

    xiala3() {
      var that = this;
      that
        .axios({
          url: `http://122.112.253.28:8095/prod-api/basedata/bdormitory/getBDormitoryListByCol?buildingNo=${that.ruleForm.buildingNo}&storey=${that.ruleForm.storey}`,
          method: "GET",
          headers: {
            Authorization: window.sessionStorage.token
          }
        })
        .then(response => {
          that.list3 = response.data.data;
        });
    },

    xiala4() {
      var that = this;
      that
        .axios({
          url:
            "http://122.112.253.28:8095/prod-api/sysset/hygienededuct/listAll",
          method: "GET",
          headers: {
            Authorization: window.sessionStorage.token
          }
        })
        .then(response => {
          // console.log(response);
          that.list4 = response.data.data;
        });
    },

    xians() {
      var that = this;
      that
        .axios({
          url:
            "http://122.112.253.28:8095/prod-api/smartdor/sdhygiene/list?pageNum=1&pageSize=10",
          method: "GET",
          headers: {
            Authorization: window.sessionStorage.token
          }
        })
        .then(response => {
          // console.log(response)
          that.jb = response.data.data.list;
        });
    },

    Delete(id) {
      var that = this;
      that
        .axios({
          url:
            "http://122.112.253.28:8095/prod-api/smartdor/sdhygiene/deleteByIds/" +
            id,
          method: "DELETE",
          headers: {
            Authorization: window.sessionStorage.token
          }
        })
        .then(response => {
          console.log(response);
          if (response.data.code == "200") {
            that.$message({
              type: "success",
              message: "删除成功"
            });
            that.xians();
          } else {
            that.$message({
              type: "info",
              message: "删除失败"
            });
          }
        });
    },

    Chax() {
      var that = this;
      that
        .axios({
          url: `http://122.112.253.28:8095/prod-api/smartdor/sdhygiene/list?pageNum=1&pageSize=10&checkDate=${that.qk.checkDate}`,
          method: "GET",
          headers: {
            Authorization: window.sessionStorage.token
          },
          data: {
            checkDate: that.qk.checkDate
          }
        })
        .then(response => {
          // console.log(response)
          that.jb = response.data.data.list;
          // that.xians();
        });
    },

    qingk() {
      this.qk = {
        checkDate: ""
      };
      this.xians();
    },

    submitForm() {
      var that = this;
      that
        .axios({
          url: "http://122.112.253.28:8095/prod-api/smartdor/sdhygiene/create",
          method: "POST",
          headers: {
            Authorization: window.sessionStorage.token
          },
          data: {
            checkDate: that.ruleForm.checkDate,
            buildingNo: that.ruleForm.buildingNo,
            storey: that.ruleForm.storey,
            bdormitoryId: that.ruleForm.dormitoryNo,
            deductIds: that.ruleForm.deductOption,
            remark: that.ruleForm.remark
          }
        })
        .then(response => {
          // console.log(response);
          if (response.data.code == "200") {
            that.$message({
              type: "success",
              message: "添加成功"
            });
            that.Xinz = false;
            that.xians();
          } else {
            that.$message({
              type: "info",
              message: "添加失败"
            });
          }
        });
    },

    Xiug(id) {
      this.dialogFormVisible2 = true;
      var that = this;
      that
        .axios({
          url: `http://122.112.253.28:8095/prod-api/smartdor/sdhygiene/${id}`,
          method: "GET",
          headers: {
            Authorization: window.sessionStorage.token
          }
        })
        .then(response => {
          that.ruleForm2 = response.data.data
          // console.log(response);
        });
    },

    Xiuggqr(){
      var that = this;
      that.axios({
        url:`http://122.112.253.28:8095/prod-api/smartdor/sdhygiene/update/${id}`,
        methdo:"PUT",
        headers:{
          Authorization:window.sessionStorage.token
        }
      })
    }
  }
};
</script>

<style scoped>
.div_d {
  width: 1641px;
  height: 848px;
}
.div_d1 {
  width: 100%;
  height: 60px;
}
.div_d2 {
  width: 270px;
  height: 58px;
  float: left;
}
.label_1 {
  width: 70px;
}
.div_d3 {
  width: 100%;
  height: 516px;
}
.div_d4 {
  margin-top: 20px;
  width: 100%;
  height: 500px;
}
.div_d6 {
  width: 400px;
  float: left;
}
.div_d7 {
  width: 400px;
  float: left;
}
.div_d8 {
  width: 160px;
  position: absolute;
  left: 681px;
  top: 414px;
}
.sb1 {
  margin-top: 10px;
}
.el_button_1 {
  margin-left: 10px;
}
.lm {
  margin-top: 10px;
}
</style>