<template>
  <el-row>
    Name：{{info.name}}
    <el-input v-model="info.name" placeholder="Please input name."></el-input>
    Age：{{info.age}}
    <el-input v-model="info.age" placeholder="Please input Age."></el-input>
    Sex：{{info.sex}}
    <el-select v-model="info.sex" placeholder="Please select">
      <el-option v-for="item in options" :key="item" :value="item"></el-option>
    </el-select>
    <el-button @click="create">Creat</el-button>
    <template>
      <el-table :data="tabledata" align="left">
        <el-table-column prop="name" label="Name"></el-table-column>
        <el-table-column prop="age" label="Age"></el-table-column>
        <el-table-column prop="sex" label="Sex"></el-table-column>
        <el-table-column label="operation">
          <template slot-scope="a">
            <el-button size="mini" type="danger" @click="del(a.$index)">del</el-button>
          </template>
        </el-table-column>
      </el-table>
    </template>
  </el-row>
</template>
<script>
import Storage from '../store/store'
export default{
  name: "NewContact",
  data(){
    return{
      info: {
        name: '',
        age: null,
        sex: ''
      },
      options: [
        'female','male','secret'
      ],
      tabledata: Storage.fetch()
    }
  },
  methods: {
    create(){
      this.tabledata.push(this.info)
      this.info = {name: '', age: null, sex: ''}
    },
    del(index){
      this.tabledata.splice(index,1)
    }
  },
  watch: {
    tabledata:{
      handler(items){Storage.save(items)},
      deep: true
    }
  }
}
</script>
<style>
    #main{
      float: none;
      margin: 0 auto;
  }
  .el-input{
    padding-bottom: 5px;
  }
  .el-select {
      display: block;
  }
  .btn-auto{
      width: 100%;
      margin-top: 12px;
  }
</style>
