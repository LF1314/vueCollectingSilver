<template>

<div class='wraper'>
    <el-row>
        <el-col :span=7 class="mypost" id='mypost'>
              <el-tabs>
                <el-tab-pane label='点餐'>
                   <el-table border style="width:100%"  :data='tableData' size='mini'>
                       <el-table-column prop='goodsName' label='食物名称'>
                           
                       </el-table-column>
                       <el-table-column prop='num' label='数量' width='50'>
                         
                       </el-table-column>
                       <el-table-column prop='price' label='单价' width='50'>
                           
                       </el-table-column>
                       <el-table-column  label='操作' fixed="right" width='100'>
                           <template slot-scope='scope'>
                               <el-button type='text'   size='small' @click="removeTabledata(scope.row)">
                                    删除
                               </el-button>
                               <el-button type='text' size='small' @click="addTabledata(scope.row)">
                                   添加
                               </el-button>
    
                           </template>

                       </el-table-column>
                   </el-table>
                </el-tab-pane>
                <el-tab-pane label='挂单'></el-tab-pane>
                <el-tab-pane label='外卖'></el-tab-pane>
              </el-tabs>
               <!-- 定义下面 数量 以及金额的总和 -->
              <div class="summoney">
                  <div>
                      <small>数量：</small>
                      <span>{{foodtotals}}</span>
                  </div>
                  <div>
                        <small>金额：￥</small>
                        <span>{{foodmoney}}</span>
                        <small>元</small>
                  </div>
              </div> 
               <div class="mybutton">
                    <el-button type="danger" size="mini">删除</el-button>
                   <el-button type='wrong' size="mini" >挂单</el-button>
                   <el-button type="success" size="mini" >结账</el-button>
                 </div>
             



        </el-col>
        <el-col :span=17>
           <div class="usallwraper">
               <div class="title">热卖食物</div>
               <div class="foodlist">
                   <ul>
                       <li v-for='(food,index) in  fooslist' :key='index' @click="addTabledata(food)">
                           <span>{{food.goodsName}}</span>
                           <span class="foodprice">￥{{food.price}}元</span>
                       </li>
                   </ul>


               </div>
 
           </div>

           <div class="typelist">
               <el-tabs>
                    <el-tab-pane label="汉堡">
                       <div class="typelistul">
                             <ul>
                             <li v-for="(food,index) in type0foods" :key="index" @click="addTabledata(food)">
                                <span class="goodimg"> <img :src="food.goodsImg" alt="" width="100%"></span>
                                 <div class="textspan">
                                     <span>{{food.goodsName}}</span>
                                 <span>￥{{food.price}}元</span>
                                 </div>
                             </li>
                            </ul>
                        </div>
                    </el-tab-pane>
                     <el-tab-pane label="小食">
                           <div class="typelistul">
                             <ul>
                             <li v-for="(food,index) in type1foods" :key="index" @click="addTabledata(food)">
                                <span class="goodimg"> <img :src="food.goodsImg" alt="" width="100%"></span>
                                 <div class="textspan">
                                     <span>{{food.goodsName}}</span>
                                 <span>￥{{food.price}}元</span>
                                 </div>
                             </li>
                            </ul>
                        </div>
                    </el-tab-pane>
                    <el-tab-pane label="饮料">
                             <div class="typelistul">
                             <ul>
                             <li v-for="(food,index) in type2foods" :key="index" @click="addTabledata(food)">
                                <span class="goodimg"> <img :src="food.goodsImg" alt="" width="100%"></span>
                                 <div class="textspan">
                                     <span>{{food.goodsName}}</span>
                                 <span>￥{{food.price}}元</span>
                                 </div>
                             </li>
                            </ul>
                        </div>
                    </el-tab-pane>
                    <el-tab-pane label="套餐">
                             <div class="typelistul">
                             <ul>
                             <li v-for="(food,index) in type3foods" :key="index" @click="addTabledata(food)">
                                <span class="goodimg"> <img :src="food.goodsImg" alt="" width="100%"></span>
                                 <div class="textspan">
                                     <span>{{food.goodsName}}</span>
                                 <span>￥{{food.price}}元</span>
                                 </div>
                             </li>
                            </ul>
                        </div>
                    </el-tab-pane>

               </el-tabs>


           </div>
        </el-col>
    </el-row>
  
</div>
    
</template>



<script>
import axios from "axios";

export default {
  name: "pos",
  data() {
    return {
      foodtotals: 0,
      foodmoney: 0,
      tableData: [],
      fooslist: [],
      type0foods: [],
      type1foods: [],
      type2foods: [],
      type3foods: []
    };
  },
  created() {
    axios
      .get(
        "https://www.easy-mock.com/mock/5b8b30dbf032f03c5e71de7f/kuaican/oftenGoods"
      )
      .then(res => {
        console.log(res);
        this.fooslist = res.data;
      })
      .catch(err => {
        console.log(err);
      });
    axios
      .get(
        "https://www.easy-mock.com/mock/5b8b30dbf032f03c5e71de7f/kuaican/typeGoods"
      )
      .then(res => {
        console.log(res);
        this.type0foods = res.data[0];
        this.type1foods = res.data[1];
        this.type2foods = res.data[2];
        this.type3foods = res.data[3];
      })
      .catch(err => {
        console.log(err);
      });
  },
  mounted: function() {
    let bodyheight = document.body.clientHeight;
    document.getElementById("mypost").style.height = bodyheight + "px";
  },
  methods: {
    //添加订餐列表
    addTabledata(good) {
      this.foodtotals = 0;
      this.foodmoney = 0;
      let ishave = false;
      let newarr = [];
      if(good){
           for (let i = 0; i < this.tableData.length; i++) {
        if (this.tableData[i].goodsId == good.goodsId) {
          ishave = true;
        }
      }
      if (ishave) {
        let arr = this.tableData.filter(item => item.goodsId == good.goodsId);
        arr[0].num++;
      } else {
        newarr[0] = {
          goodsId: good.goodsId,
          goodsName: good.goodsName,
          price: good.price,
          num: 1
        };
      }
      this.tableData = [...this.tableData, ...newarr];
      }
      this.tableData.forEach(item => {
        this.foodmoney += item.price * item.num;
        this.foodtotals += item.num;
      });
    },
    removeTabledata(good) {
      let obj = this.tableData.map((item, index) => {
        if (item.goodsId == good.goodsId) {
          //   this.tableData.splice(index, 1);
          if (item.num == 1) {
            this.tableData.splice(index, 1);
          } else {
            item.num--;
          }
        }
        return item;
      });
      this.addTabledata();
    }
  }
};
</script>



<style scoped>
.summoney {
  font-size: 16px;
  line-height: 40px;
  height: 40px;
  border-bottom: 1px solid #e4e7ed;
  display: flex;
  justify-content: space-around;
}
.typelist {
  padding-left: 10px;
}
.typelistul ul li {
  display: inline-block;
  padding: 5px;
}
.typelistul li {
  text-align: center;
  font-size: 14px;
  overflow: hidden;

  margin: 0;
  padding: 0;
}
.typelistul li:hover {
  cursor: pointer;
}
.typelistul span {
  display: block;
  width: 80px;

  float: left;
}
.textspan span:nth-child(1) {
  width: 100px;
}
.typelistul .textspan {
  background-color: #fff;
  float: right;
  overflow: hidden;
  width: 100px;
  line-height: 35px;
  padding: 5px;
}
.wraper {
  width: 100%;
  height: 100%;
}
.mypost {
  background-color: #fff;
  font-size: 19px;
  text-align: center;
}
.mybutton {
  margin-top: 20px;
}
.title {
  height: 37px;
  background-color: #fff;
  font-size: 15px;
  text-align: left;
  line-height: 37px;
  border-left: 2px solid #f2f2f2;
  padding-left: 10px;
  border-bottom: 2px solid #e4e7ed;
}
.foodlist ul {
  border-bottom: 2px solid #e4e7ed;
}
.foodlist ul li {
  display: inline-block;
  margin: 10px;
  padding: 7px;
  font-size: 14px;
  background-color: #fff;
  list-style: none;
  border-radius: 2px;
}
.foodlist ul li:hover {
  cursor: pointer;
}
.foodprice {
  font-size: 11px;
  color: #666;
}
</style>

