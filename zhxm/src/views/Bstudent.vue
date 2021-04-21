<template>
  <div class="div_d">
    <div class="div_d1">
      <div class="demo-input-suffix div_d2">
        学员名称：
        <el-input placeholder="请输入学员名称" v-model="qk.studentName" clearable class="el_input_1"></el-input>
      </div>

      <div class="demo-input-suffix div_d2">
        <label for>学号：</label>
        <el-input placeholder="请输入学号" v-model="qk.studentNo" clearable class="el_input_1"></el-input>
      </div>

      <div class="demo-input-suffix div_d2">
        <label for>班级：</label>
        <el-input placeholder="请输入班级" v-model="qk.className" clearable class="el_input_1"></el-input>
      </div>

      <div class="demo-input-suffix div_d2">
        <label for>宿舍栋号：</label>
        <el-select v-model="qk.buildingNo" placeholder="请输入宿舍栋号">
          <el-option
            v-for="(item1,key1) in list1"
            :key="key1"
            :value="item1.dictSort"
          >{{item1.dictLabel}}</el-option>
        </el-select>
      </div>

      <div class="demo-input-suffix div_d2">
        <label for>宿舍楼层：</label>
        <el-select v-model="qk.storey" placeholder="请输入宿舍楼层">
          <el-option
            v-for="(item2,key2) in list2"
            :key="key2"
            :value="item2.dictSort"
          >{{item2.dictLabel}}</el-option>
        </el-select>
      </div>

      <div class="demo-input-suffix div_d2">
        <label for>宿舍号：</label>
        <el-input placeholder="请输入宿舍号" v-model="qk.dormitoryNo" clearable class="el_input_1"></el-input>
      </div>

      <div class="demo-input-suffix div_d2">
        <label for>状态：</label>
        <el-select v-model="qk.status" placeholder="学员状态">
          <el-option
            v-for="(item3,key3) in list3"
            :key="key3"
            :value="item3.status"
          >{{item3.dictLabel}}</el-option>
        </el-select>
      </div>
      <el-button type="primary" icon="el-icon-search" @click="Chax">查询</el-button>
      <el-button plain icon="el-icon-refresh" @click="qingk">重置</el-button>
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
          ref="ruleForm"
          label-width="100px"
          class="demo-ruleForm"
        >
          <div class="div_d6">
            <div class="demo-input-suffix">
              <el-form-item label="学员姓名">
                <el-input v-model="ruleForm.studentName" placeholder="请输入学员姓名"></el-input>
              </el-form-item>
            </div>

            <div class="demo-input-suffix sb1">
              班级
              <el-select v-model="ruleForm.className" placeholder="请输入班级">
                <el-option
                  v-for="(item4, key4) in list4"
                  :key="key4"
                  :value="item4.dictValue"
                >{{item4.dictLabel}}</el-option>
              </el-select>
            </div>

            <div class="demo-input-suffix sb1">
              <el-form-item label="身份证号">
                <el-input v-model="ruleForm.idcard" placeholder="请输入身份证号"></el-input>
              </el-form-item>
            </div>

            <div class="demo-input-suffix sb1">
              <el-form-item label="年龄">
                <el-input v-model="ruleForm.age" placeholder="请输入年龄"></el-input>
              </el-form-item>
            </div>

            <div class="demo-input-suffix sb1">
              <el-form-item label="家长电话">
                <el-input v-model="ruleForm.parentPhone" placeholder="请输入家长电话"></el-input>
              </el-form-item>
            </div>

            <div class="demo-input-suffix sb1">
              宿舍楼层
              <el-select v-model="ruleForm.sex" placeholder="请输入宿舍楼层">
                <el-option
                  v-for="(item4, key4) in list4"
                  :key="key4"
                  :value="item4.dictValue"
                >{{item4.dictLabel}}</el-option>
              </el-select>
            </div>
          </div>

          <div class="div_d7">
            <div class="demo-input-suffix sb1">
              <el-form-item label="学号">
                <el-input v-model="ruleForm.studentNo"></el-input>
              </el-form-item>
            </div>

            <div class="demo-input-suffix sb1">
              <el-form-item label="手机号码">
                <el-input v-model="ruleForm.phone" placeholder="请输入手机号码"></el-input>
              </el-form-item>
            </div>

            <div class="demo-input-suffix sb1">
              性别
              <el-select v-model="ruleForm.sex" placeholder="请输入性别">
                <el-option
                  v-for="(item4, key4) in list4"
                  :key="key4"
                  :value="item4.dictValue"
                >{{item4.dictLabel}}</el-option>
              </el-select>
            </div>

            <div class="demo-input-suffix sb1">
              <el-form-item label="家长姓名">
                <el-input v-model="ruleForm.parentName" placeholder="请输入家长姓名"></el-input>
              </el-form-item>
            </div>

            <div class="demo-input-suffix sb1">
              宿舍栋号
              <el-select v-model="ruleForm.buildingNo" placeholder="请输入宿舍栋号">
                <el-option
                  v-for="(item4, key4) in list4"
                  :key="key4"
                  :value="item4.dictValue"
                >{{item4.dictLabel}}</el-option>
              </el-select>
            </div>

            <div class="demo-input-suffix sb1">
              宿舍号
              <el-select v-model="ruleForm.dormitoryNo" placeholder="请输入宿舍号">
                <el-option
                  v-for="(item4, key4) in list4"
                  :key="key4"
                  :value="item4.dictValue"
                >{{item4.dictLabel}}</el-option>
              </el-select>
            </div>
          </div>
        </el-form>
        <div class="demo-input-suffix div_d8">
          <span slot="footer" class="dialog-footer">
            <el-button @click="Xinz = false">取 消</el-button>
            <el-button type="primary" @click="submitForm('ruleForm')">确 定</el-button>
          </span>
        </div>
      </el-dialog>

      <div class="div_d4">
        <el-table ref="multipleTable" :data="jb" tooltip-effect="dark" style="width: 100%">
          <el-table-column type="selection" width="55"></el-table-column>
          <el-table-column label="序号" width="120">
            <template slot-scope="scope">{{ scope.row.id }}</template>
          </el-table-column>
          <el-table-column prop="studentName" label="学员姓名"></el-table-column>
          <el-table-column prop="studentNo" label="学号"></el-table-column>
          <el-table-column prop="className" label="班级"></el-table-column>
          <el-table-column prop="phone" label="手机号"></el-table-column>
          <el-table-column label="性别">
            <template slot-scope="scope">{{scope.row.sex === 1 ? '女' : '男'}}</template>
          </el-table-column>
          <el-table-column prop="parentName" label="家长姓名"></el-table-column>
          <el-table-column prop="parentPhone" label="家长来电"></el-table-column>
          <el-table-column prop="buildingNo" label="宿舍栋号"></el-table-column>
          <el-table-column prop="storey" label="楼层"></el-table-column>
          <el-table-column prop="dormitoryNo" label="宿舍号"></el-table-column>
          <el-table-column prop="modifyTime" label="创建时间"></el-table-column>
          <el-table-column prop="status" label="状态">
            <template slot-scope="scope">
              <div>
                <div style="position:relative;z-index:999">
                  <el-switch
                    v-model="scope.row.status"
                    active-color="#13ce66"
                    inactive-color="#ff4949"
                  ></el-switch>
                </div>
              </div>
            </template>
          </el-table-column>
          <el-table-column label="操作">
            <template slot-scope="scope">
              <el-button type="success" icon="el-icon-edit" circle @click="update(scope.row.id)"></el-button>
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
      list1: [],
      list2: [],
      list3: [],
      list4: [],
      qk: {
        studentName: "",
        studentNo: "",
        className: "",
        dormitoryNo: ""
      },

      buildingNo: "",
      storey: "",
      status: "",

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
      ruleForm: {
        studentName: "",
        studentNo: ""
      },
      pageNum: 1,
      pageSize: 100
    };
  },
  mounted() {
    this.xiala1();
    this.xiala2();
    this.xiala3();
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
          url:
            "http://122.112.253.28:8095/prod-api/sys/dict/detail/dictType/sys_student_status",
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
            "http://122.112.253.28:8095/prod-api/sys/dict/detail/dictType/sys_user_sex",
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
            "http://122.112.253.28:8095/prod-api/basedata/bstudent/list?pageNum=1&pageSize=10",
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
            "http://122.112.253.28:8095/prod-api/basedata/bstudent/deleteByIds/" +
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
          url: `http://122.112.253.28:8095/prod-api/basedata/bstudent/list?pageNum=1&pageSize=10&studentName=${that.qk.studentName}&studentNo=${that.qk.studentNo}&className=${that.qk.className}&dormitoryNo=${that.qk.dormitoryNo}`,
          method: "GET",
          headers: {
            Authorization: window.sessionStorage.token
          },
          data: {
            studentName: that.qk.studentName,
            studentNo: that.qk.studentNo,
            className: that.qk.className,
            dormitoryNo: that.qk.dormitoryNo
          }
        })
        .then(response => {
          // console.log(response)
          that.jb = response.data.data.list;
        });
    },

    qingk() {
      this.qk = {
        studentName: "",
        studentNo: "",
        className: "",
        dormitoryNo: ""
      };
      this.xians();
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
  height: 116px;
}
.div_d2 {
  width: 270px;
  height: 58px;
  float: left;
}
.el_input_1 {
  width: 180px;
  height: 32px;
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
</style>