<template>
  <div class="home">
  <el-dialog title="新增" :visible.sync="dialogFormVisible">
  <el-form :model="form">
    <el-form-item label="姓名" :label-width="formLabelWidth">
      <el-input v-model="form.name" auto-complete="off"></el-input>
    </el-form-item>
    <el-form-item label="性别" :label-width="formLabelWidth">
      <el-select v-model="form.sex" placeholder="请选择">
        <el-option label="男" value="男"></el-option>
        <el-option label="女" value="女"></el-option>
        
      </el-select>
    </el-form-item>
  </el-form>
  {{form}}
  <div slot="footer" class="dialog-footer">
    <el-button @click="dialogFormVisible = false">取 消</el-button>
    <el-button type="primary" @click="submit">确 定</el-button>
  </div>
</el-dialog>

  <el-button @click="tanchu" type="success" v-if="'1'==$route.params.state">+</el-button>
    <el-table
      :data="tableData"
      style="width: 100%">
      <el-table-column
        prop="id"
        label="日期"
        width="180">
      </el-table-column>
      <el-table-column
        prop="name"
        label="姓名"
        width="180">
      </el-table-column>
      <el-table-column
        prop="sex"
        label="地址">
      </el-table-column>
      <el-table-column
        prop="sex"
        label="操作">
        <template slot-scope="scope">
        <el-button
          @click.native.prevent="deleteRow(scope.row, 1)"
          type="text"
          size="small">
          移除
        </el-button>
      </template>
      </el-table-column>
    </el-table>
  </div>
</template>


// @ is an alias to /src
<script>
    export default {
      data() {
        return {
          tableData: [],
          dialogFormVisible: false,
          form:{
            name:"",
            sex:""
          },
          formLabelWidth:"120px"
        }
      },
      methods:{
        submit(){
          this.dialogFormVisible = false
          this.$http.post('http://localhost:3000/add',this.form,{emulateJSON:true}).then(function(){
            this.J_fetch()
            this.form={}
            this.$message({
          message: '恭喜你，这是一条成功消息',
          type: 'success'
        });
          })
        },
        tanchu(){
          this.dialogFormVisible = true
        },
        deleteRow(e,i){
          console.log(e)
          this.$http.post('http://localhost:3000/del',{id:e.id},{emulateJSON:true}).then(function(){
            var _index=this.tableData.indexOf(e)
            this.tableData.splice(_index,1)
            this.$message({
          message: '恭喜你，删除成功',
          type: 'success'
        });
          })
        },
        J_fetch(){
          this.$http.post('http://localhost:3000',{state:this.$route.params.state},{emulateJSON:true}).then(e=>this.tableData=e.body)
        }
      },
      watch:{
        '$route':function(){
          this.J_fetch()
        }
      },
      created(){
        this.J_fetch()
      }
    }

</script>
