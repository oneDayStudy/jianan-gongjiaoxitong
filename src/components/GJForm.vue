<template>
  <div id='form'>
  <el-container>
      <!-- 列表 -->
         <el-aside width="200px">
           
            <el-tree
            class='filter-tree'
            :data='data2'
            :props='defaultProps'
            default-expand-all
            ref='tree2'>
            </el-tree>

         </el-aside>
      <!-- contaner -->
      <el-container>
         <!-- header -->
      <el-header>
        <el-button  type="primary" v-on:click='saveEdit'>{{header[0]}}</el-button>
        <el-button  type="primary">{{header[1]}}</el-button>
        <el-button  type="primary">{{header[2]}}</el-button>
        <el-button  type="primary">{{header[3]}}</el-button>
        <el-button  type="primary">{{header[4]}}</el-button>
        <el-button  type="primary">{{header[5]}}</el-button>
        <el-button  type="primary">{{header[6]}}</el-button>
        <el-button  type="primary">{{header[7]}}</el-button>
        <el-button  type="primary">{{header[8]}}</el-button>
      </el-header>
         <!-- 内容 -->
         <el-main>
           <el-table :data='tableData' border style='width:100%' class='table'>
             <!-- <el-table-column fixed prop='itemId'  label=" " width='150'></el-table-column>   -->
             <el-table-column  label='上行序号' width='150' style="position:relative">
               <template slot-scope="scope">
                  <!-- <i class="el-icon-time"></i> -->
                  <input v-model="editArr.shNum"  v-show='scope.row.itemId==nowEditCol'>
                   
                  <span>{{scope.row.itemId}}-{{editArr.title}}</span> 
               </template>
               </el-table-column>  
             <el-table-column   label='上行站点' width='150'>
               <template slot-scope="scope">
                  <!-- <i class="el-icon-time"></i> -->
                  <input v-model="editArr.shNum"  v-show='scope.row.itemId==nowEditCol'>
                  <span>{{scope.row.shName}}</span> 
               </template>
             </el-table-column>  
             <el-table-column   label='上行英文名' width='150'>
               <template slot-scope="scope">
                  <!-- <i class="el-icon-time"></i> -->
                  <input v-show='scope.row.itemId==nowEditCol'>
                  <span>{{scope.row.shEName}}</span> 
               </template>
               </el-table-column>  
             <el-table-column   label='上行首末站' width='150'>
               <template slot-scope="scope">
                  <!-- <i class="el-icon-time"></i> -->
                  <input v-show='scope.row.itemId==nowEditCol'>
                  <span>{{scope.row.shFirsLas}}</span> 
               </template>
               </el-table-column>  
             <el-table-column   label='上行首末站英文' width='150'>
               <template slot-scope="scope">
                  <!-- <i class="el-icon-time"></i> -->
                  <input v-show='scope.row.itemId==nowEditCol'>
                  <span>{{scope.row.shEFirsLas}}</span> 
               </template>
               </el-table-column>  
             <el-table-column   label='下行序号' width='150'>
                <template slot-scope="scope">
                  <!-- <i class="el-icon-time"></i> -->
                  <input v-show='scope.row.itemId==nowEditCol'>
                  <span>{{scope.row.xhNum}}</span> 
               </template>
               </el-table-column>  
             <el-table-column   label='下行站点' width='150'>
                <template slot-scope="scope">
                  <!-- <i class="el-icon-time"></i> -->
                  <input v-show='scope.row.itemId==nowEditCol'>
                  <span>{{scope.row.xhName}}</span> 
               </template>
               </el-table-column>  
             <el-table-column   label='下行英文名' width='150'>
                <template slot-scope="scope">
                  <!-- <i class="el-icon-time"></i> -->
                  <input v-show='scope.row.itemId==nowEditCol'>
                  <span>{{scope.row.xhEName}}</span> 
               </template>
               </el-table-column>  
             <el-table-column   label='下行首末站' width='150'>
                 <template slot-scope="scope">
                  <!-- <i class="el-icon-time"></i> -->
                  <input v-show='scope.row.itemId==nowEditCol'>
                  <span>{{scope.row.xhFirsLas}}</span> 
                </template>
               </el-table-column>  
             <el-table-column   label='下行首末站英文' width='150'>
               <template slot-scope="scope">
                  <!-- <i class="el-icon-time"></i> -->
                  <input v-show='scope.row.itemId==nowEditCol'>
                  <span>{{scope.row.xhEFirsLas}}</span> 
                </template>
               </el-table-column>  
             <el-table-column   label='宣传语序号' width='150'>
               <template slot-scope="scope">
                  <!-- <i class="el-icon-time"></i> -->
                  <input v-show='scope.row.itemId==nowEditCol'>
                  <span>{{scope.row.xuanNum}}</span> 
                </template>
               </el-table-column>  
             <el-table-column   label='宣传用语' width='150'>
               <template slot-scope="scope">
                 
                  <input type="text" style="" v-show='scope.row.itemId==nowEditCol'>
                  <span>{{scope.row.xuanchuan}}</span> 
                </template>
               </el-table-column>  
             <el-table-column   label='宣传用语英文' width='150'>
               <template slot-scope="scope">
                 
                  <input type="text" v-show='scope.row.itemId==nowEditCol'>
                  <span>{{scope.row.xuanchuan}}</span> 
                </template>
               </el-table-column>  
             <el-table-column  fixed='right' label='编辑' width='150'>
                <template slot-scope='scope'>
                  
                    <el-button size='mini' @click='startEdit(scope.row.itemId)'>编辑</el-button>  
                    <el-button size='mini' @click='cancelEdit'>取消</el-button>  
                    <el-button size='mini' @click='sureEdit(scope.row.itemId)'>确定</el-button>  
                    <el-button size='mini' type="danger" @click='handleDelete(scope.$index,scope.row)'>删除</el-button>  
                  </template>  
             </el-table-column>  

           </el-table>
         </el-main>
      </el-container>
  </el-container>
  </div>
</template>

<script>
export default {
  created(){
    // this.$http.get(
    //   '@/assets/logo.png').then((res)=>{
    //   console.log(res)
    // }).catch((res)=>{console.log(res.status)})
   
  },
 
  methods:{
    saveEdit(){
    //模拟保存成功 
    this.$message('保存成功');
    },
    handleEdit(index,row){
      console.log(index,row)
      console.log(this)
      this.ipt = true;
    },
    handleDelete(){},
    startEdit(id){
        this.nowEditCol=id
    },
    cancelEdit(){
         this.nowEditCol=-1
    },
    sureEdit(id){
      // console.log(this.tableData,id)
       console.log(this.editArr)
     for(var i=0,len=this.tableData;i<len;i++){
        if(id === this.tableData[i][itemId]){
          this.tableData.splice(i,1,this.editArr);
         
          break;
        }
     }
       this.nowEditCol=-1
    },

  },
  data () {
    return {
     header:["保存工程","进站播报","出站播报","宣传语播报","多行表格删除","多行表格增加","一键删除宣传语","编辑","取消",],
     filterText:'',
     tableHeader:["上行序号","上行站点","上行英文名","上行首末站","上首末英文","下行序号","下行站点","下行英文名","下行首末站","下首英文名","宣传语序号","宣传用语","宣传语英文","编辑"],

     ipt:false,
     nowEditCol:-1,

     tableData:[
      {	
					"itemId":"002",
					"nowRun":false,
					"shNum":"2",
					"shName":"名都花园",
					"shEName":"keyunzhan",
					"shFirsLas":" ",
					"shEFirsLas":" ",
					"xhNum":"1",
					"xhName":"东张",
					"xhEName":"dongzhang",
					"xhFirsLas":" ",
					"xhEFirsLas":" ",
					"xuanNum":"1",
					"xuanchuan":"乘客们请照顾老弱病残",
					"EngliXuanchuan":"乘客们请照顾老弱病残",
					"title":""
        },
        {	
					"itemId":"012",
					"nowRun":false,
					"shNum":"2",
					"shName":"名都花园",
					"shEName":"keyunzhan",
					"shFirsLas":" ",
					"shEFirsLas":" ",
					"xhNum":"1",
					"xhName":"东张",
					"xhEName":"dongzhang",
					"xhFirsLas":" ",
					"xhEFirsLas":" ",
					"xuanNum":"1",
					"xuanchuan":"乘客们请照顾老弱病残",
					"EngliXuanchuan":"乘客们请照顾老弱病残",
					"title":""
        },
        {	
					"itemId":"003",
					"nowRun":false,
					"shNum":"2",
					"shName":"名都花园",
					"shEName":"keyunzhan",
					"shFirsLas":" ",
					"shEFirsLas":" ",
					"xhNum":"1",
					"xhName":"东张",
					"xhEName":"dongzhang",
					"xhFirsLas":" ",
					"xhEFirsLas":" ",
					"xuanNum":"1",
					"xuanchuan":"乘客们请照顾老弱病残",
					"EngliXuanchuan":"乘客们请照顾老弱病残",
					"title":""
        },
        {	
					"itemId":"004",
					"nowRun":false,
					"shNum":"2",
					"shName":"名都花园",
					"shEName":"keyunzhan",
					"shFirsLas":" ",
					"shEFirsLas":" ",
					"xhNum":"1",
					"xhName":"东张",
					"xhEName":"dongzhang",
					"xhFirsLas":" ",
					"xhEFirsLas":" ",
					"xuanNum":"1",
					"xuanchuan":"乘客们请照顾老弱病残",
					"EngliXuanchuan":"乘客们请照顾老弱病残",
					"title":""
				},
     ],
     data2:[{
       id:1,
       label:'工程',
       children:[{
         id:4,
         label:'工程目录列表',
         children:[{id:5,label:'1203'},{id:5,label:'2312'},{id:5,label:'1303'},{id:5,label:'1103'}]
       }]
     }],
     defaultProps:{
       children:'children',
       label:'label'
     }
    }
  },
   computed:{
    editArr:function(){
      var editO ={};
      for(var i=0,len=this.tableData.length;i<len;i++){
          if(this.nowEditCol === this.tableData[i]['itemId']){
              editO = this.tableData[i];
              break;
          }
      } 
      return {
        	"itemId":editO.itemId,
					"nowRun":editO.nowRun,
					"shNum":editO.shNum,
					"shName":editO.shName,
					"shEName":editO.shEName,
					"shFirsLas":editO.shFirsLas,
					"shEFirsLas":editO.shEFirsLas,
					"xhNum":editO.xhNum,
					"xhName":editO.xhName,
					"xhEName":editO.xhEName,
					"xhFirsLas":editO.xhFirsLas,
					"xhEFirsLas":editO.xhEFirsLas,
					"xuanNum":editO.xuanNum,
					"xuanchuan":editO.xuanchuan,
					"EngliXuanchuan":editO.EngliXuanchuan,
					"title":""
      }
    }
  },
}
</script>
<style scoped>
   .el-header, .el-footer {
    background-color: #B3C0D1;
    color: #333;
    text-align: center;
    line-height: 60px;
  }
  
  .el-aside {
    background-color: #D3DCE6;
    color: #333;
    text-align: center;
    line-height: 200px;
  }
  
  .el-main {
    background-color: #E9EEF3;
    color: #333;
    text-align: center;
    line-height: 160px;
  }

  /* form */
  .table :nth-child(2){
   
  }

  .el-table{line-height:50px}
  .el-table input{ line-height:50px; position:absolute;width:100%;height:100%;left:0;top:0;margin:0;padding:0;}
  .el-table span{margin-left:10px;}

.mytd{
  position: relative;
}
.myipt{
  position: absolute;
}
.cell{background:rgb(44, 44, 126)violet}

</style>
