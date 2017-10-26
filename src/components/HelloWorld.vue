<template>
  <div class="hello">
    <input type="button" value="主题1" @click="con(1)"/> 
    <input type="button" value="主题2" @click="con(2)"/> 
    <div ref="root">
      <p>我是父亲一段话</p>
      <div class="son">
        <p>我是儿子一段话</p>
      </div>
    </div> 

    <v-table
      is-horizontal-resize
      style="width:100%"
      :columns="columns"
      :table-data="tableData"
      :show-vertical-border="false"
      :multiple-sort="multipleSort"
      row-hover-color="rgba(39,157,218,.2)"
      row-click-color="#edf7ff"
    ></v-table>
  </div>
</template>

<script>
import Vue from 'vue'
import axios from 'axios'
import 'vue-easytable/libs/themes-base/index.css'
import {VTable, VPagination} from 'vue-easytable'

Vue.component(VTable.name, VTable)
Vue.component(VPagination.name, VPagination)

export default {
  name: 'HelloWorld',
  data () {
    return {
      userDataList: [],
      msg: 'Welcome to Your Vue.js App',
      tableData: [
        {'name': '赵伟', 'tel': '156*****1987', 'hobby': '钢琴、书法、唱歌', 'address': '上海市黄浦区金陵东路569号17楼'},
        {'name': '李伟', 'tel': '182*****1538', 'hobby': '钢琴、书法、唱歌', 'address': '上海市奉贤区南桥镇立新路12号2楼'},
        {'name': '孙伟', 'tel': '161*****0097', 'hobby': '钢琴、书法、唱歌', 'address': '上海市崇明县城桥镇八一路739号'},
        {'name': '周伟', 'tel': '197*****1123', 'hobby': '钢琴、书法、唱歌', 'address': '上海市青浦区青浦镇章浜路24号'},
        {'name': '吴伟', 'tel': '183*****6678', 'hobby': '钢琴、书法、唱歌', 'address': '上海市松江区乐都西路867-871号'}
      ],
      columns: [
        {width: 60, titleAlign: 'center', columnAlign: 'center', type: 'selection'},
        {field: 'name', title: '姓名', width: 100, titleAlign: 'center', columnAlign: 'center'},
        {field: 'tel', title: '手机号码', width: 260, titleAlign: 'center', columnAlign: 'center'},
        {field: 'hobby', title: '爱好', width: 330, titleAlign: 'center', columnAlign: 'center'},
        {field: 'address', title: '地址', titleAlign: 'center', columnAlign: 'left'}
      ]
    }
  },
  created () {
    console.log(11)
    axios.post('http://localhost:4049/whapi/User/loadcusers')
    .then(res => {
      console.log(res, 'res')
    })
  },
  methods: {
    con (n) {
      this.$refs.root.className = 'father' + n
    },
    selectALL (selection) { // 全选后触发，回调参数为 selection，已选项
      console.log('select-aLL', selection)
    },
    selectChange (selection, rowData) { // 选中某一项触发，回调参数为 selection 和 rowData，分别为已选项和刚选择的项
      console.log('select-change', selection, rowData)
    },
    selectGroupChange (selection) { // 任意选中项发生变化时就会触发，回调参数为 selection，已选项。
      console.log('select-group-change', selection)
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="less">
@import "../assets/less/theme1";
@import "../assets/less/theme2";
</style>
