<template>

<div class='wraper'>
    <el-row>
        <el-col :span=8 class="mypost" id='mypost'>
              <el-tabs>
                <el-tab-pane label='点餐'>

                   <el-table border style="width:100%" show-summary :data='foos' size='mini'>
                       <el-table-column prop='goodsname' label='食物名称'>
                           
                       </el-table-column>
                       <el-table-column prop='num' label='数量' width='50'>
                         
                       </el-table-column>
                       <el-table-column prop='price' label='单价' width='50'>
                           
                       </el-table-column>
                       <el-table-column  label='操作' fixed="right" width='100'>
                           <template slot-scope='scope'>
                               <el-button type='text'   size='small'>
                                   删除
                               </el-button>
                               <el-button type='text' size='small'>
                                   添加
                               </el-button>
                               
                           </template>

                       </el-table-column>
                   </el-table>
                 <div class="mybutton">
                    <el-button type="danger" size="mini">删除</el-button>
                   <el-button type='wrong' size="mini" >挂单</el-button>
                   <el-button type="success" size="mini" >结账</el-button>
                 </div>
                </el-tab-pane>
                <el-tab-pane label='挂单'></el-tab-pane>
                <el-tab-pane label='外卖'></el-tab-pane>

              </el-tabs>  
        </el-col>
        <el-col :span=7>
            产品列表
        </el-col>
    </el-row>
  
</div>
    
</template>



<script>

export default{
    name:'pos',
    data(){
        return{
            foos:[
                {
                    goodsname:'汉堡',
                    num:2,
                    price:12
                }
            ]
               
        }
    },
    mounted:function(){
        let bodyheight = document.body.clientHeight;
        document.getElementById('mypost').style.height=bodyheight+'px'
    }
}
    
</script>



<style scoped>
.wraper{
    width: 95%;
    height: 100%
}
.mypost{
    background-color: #fff;
    font-size: 19px;
    text-align: center;
   
}
.mybutton{
    margin-top: 20px;
}

</style>

