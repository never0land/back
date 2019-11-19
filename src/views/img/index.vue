<template>
  <div>
    <el-container style="position:absolute;top:55px;left:0;right:0;bottom:0">
      <el-header class="img_index_head">
        <!--顶部删选组件-->
        <div style="display:flex;margin-right:auto">
        <el-select v-model="search_data.select_val" placeholder="请选择图片排序方式" size="mini">
          <el-option label="区域一" value="shanghai"></el-option>
          <el-option label="区域二" value="shanghai"></el-option>
        </el-select>
        <el-input size="mini" style="width:150px;margin-right:2rem" placeholder="请输入相册名称" v-model="search_data.input_val"></el-input>
        <el-button type="success" size="mini">搜索</el-button>
        </div>
        <el-button type="success" size="mini" @click="openalbumsmodel(false)">创建相册</el-button>
        <el-button type="warning" size="mini">上传图片</el-button>
      </el-header>
    <el-container>
    <el-aside width="200px" class="img_index_aside">
      <div >
        <ul style="background-color:white;border:white">
        <li  v-for="(item,index) in albums" :key="index" @click.stop="albumsIndex(index)">
        {{item.name}}
        <el-dropdown style="margin-left:auto">
        <el-button size="small" plain>
          3<i class="el-icon-arrow-down el-icon--right"></i>
        </el-button>
      <el-dropdown-menu slot="dropdown">
        <el-dropdown-item  @click.stop.native="albumedit({item,index})">修改</el-dropdown-item>
        <el-dropdown-item @click.stop.native="albumsDel(index)">删除</el-dropdown-item>
        <!--停止默认行为，并且用原生点击事件-->
      </el-dropdown-menu>
    </el-dropdown>
        </li>
        </ul>
      </div>
    </el-aside>
    <el-container>
    <el-main class="img_index_main">
    </el-main>
    </el-container>
    </el-container>
      <el-footer>Footer
      </el-footer>
    </el-container>
    <!--修改and创建相册-->
    <el-dialog title="修改相册" :visible.sync="albumsmodel" width="30%" >
    <el-form ref="form" :model="albumsform" label-width="78px">
    <el-form-item label="相册名称">
    <el-input v-model="albumsform.name" size="medium" placeholder="请输入相册名称"></el-input>
    </el-form-item>
        <el-form-item label="label">
     <el-input-number v-model="albumsform.order" :min="0"
     size="medium"></el-input-number>
     <!--这货可以绑定最大值和最小值，而不是像原生一样绑定最大长度和最小长度-->
    </el-form-item>
    </el-form>
  <span slot="footer" class="dialog-footer">
    <el-button @click="albumsmodel = false">取 消</el-button>
    <el-button type="primary" @click="confirmalbummodel()">确 定</el-button>
  </span>
</el-dialog>
  </div>
</template>
<script>
export default {
  data () {
    return{
      albumsform:{
        name:"",
        order:0
      },
      num:1,
      albumeditindex:-1,
      //如果大于-1那么就是编辑，否则就是创建相册
      albumsChange:0,
       albums:[],
       albumsmodel:false,
      search_data:{
        select_val:'',
        input_val:''
      }
      }
  },
  created(){
    this.__init()
  },
  methods:{
    openalbumsmodel(obj){
      //打开相册修改对话框，等待用户输入键值
      console.log(obj)
      if(obj){
      let {item,index} =obj
      //初始化表单
      this.albumsform.name = item.name
      this.albumsform.order = item.order
      this.albumeditindex = index
      //打开模态框
      return this.albumsmodel = true
      }
      //创建相册
      this.albumsform = {
        name:"",
        order:0
      }
    this.albumeditindex = -1
    this.albumsmodel =true
    },
__init(){
  for(var i=0;i<20;i++){
    this.albums.push({
      name:"name"+i,
      num:Math.floor(Math.random()*100)
    })
  }
  console.log(this.albums)
},
albumsIndex(index){
  this.albumsChange =index
  //效果是有的，但是因为css没加点击前的高亮和点击后的高亮，所以看上去什么鬼都没有
  console.log(index)
},
albumsDel(index){
        this.$confirm('此操作将永久删除该相册, 是否继续?', '提示', {
          confirmButtonText: '确定',
          cancelButtonText: '取消',
          type: 'warning'
        }).then(() => {
          this.albums.splice(index,1)
          this.$message({
            type: 'success',
            message: '删除成功!'
          });
        }).catch(() => {
          this.$message({
            type: 'info',
            message: '已取消删除'
          });          
        });
      }
  //接收点击行数，并把那个删了
},
//修改相册
albumedit(item,index){
  this.albums[this.albumeditindex].name =this.albumform.name
  this.albums[this.albumeditindex].order =this.albumform.order
},
confirmalbummodel(){
  //判断客户做了什么，是不是修改
  if(this.albumeditindex > -1){
    this.albumedit()
    return this.albumsmodel = false
  }
  this.albums.unshift({
    name:this.albumform.name,
    order:this.albumform.order,
    num:0
  })
  this.albumsmodel =false
}

  }
</script>
<style scoped>
.img_index_aside{
  position:absolute;
  top:60px;
  left:0;
  bottom:60px;
}
.img_index_aside li{
  list-style:none;
  margin:5px;
  padding:5px;
  display:flex;
  align-items:center;
  height:40px;
}
.img_index_main{
  position:absolute;
  top:60px;
  left:200px;
  bottom:60px;
  right:0px;
}
.img_index_head{
  display:flex; 
  align-items:center;
}
</style>