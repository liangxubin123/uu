<template>
  <div>
    <el-button type="primary" @click="willAdd">添加</el-button>

    <v-list :list="list" @init="init" @edit="edit"></v-list>

    <v-form :info="info" @init="init" ref="form"></v-form>
  </div>
</template>
<script>
import { mapGetters, mapActions } from "vuex";
import vList from "./components/list.vue"
import vForm from "./components/form.vue"
import {reqRoleList} from "../../utils/http"
export default {
    components:{
    vList,
    vForm
  },
  data(){
    return{
 info:{
  isshou:false,
  title:"添加角色"
},
  //19.列表数据初始值
list:[]
    }
  },
  computed: {
    ...mapGetters({})
  },
  methods: {
    ...mapActions({}),
     //5.点击了添加按钮
    willAdd(){
      this.info={
        isshow:true,
        title:"添加角色"
      }
    },
    init(){
      reqRoleList().then(res=>{
        this.list=res.data.list
      })

  },
  //36 编辑
    edit(id){
      this.info={
        isshow:true,
        title:"编辑角色"
      }
      this.$refs.form.getOne(id)
    }
  },
  mounted() {
    this.init()
  }

};
</script>
<style scoped>
</style>