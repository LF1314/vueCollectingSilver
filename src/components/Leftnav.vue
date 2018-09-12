<template>
  <div class="nav">
      <ul>
        <li>
            <i class="icon iconfont icon-dianpu"></i>
            <div>店铺</div>
        </li>
        <li>
            <i class="icon iconfont icon-hanbao"></i>
            <div>食物</div>
        </li>
        <li>
            <i class="icon iconfont icon-goumai"></i>
            <div>
              收银
            </div>
        </li>
        <li>
            <i class="icon iconfont icon-huiyuanqia"></i>
            <div>
                会员
            </div>
        </li>
        <li>
            <i class="icon iconfont icon-gongnengjianyi"></i>
            <div>
                 设置
            </div>
        </li>
      </ul>

    </div>

    
</template>



<script>
export default {
  name: "Leftnav"
};
</script>



<style scoped>

.nav{
    height: 100%;
    width: 5%;
    float: left;
    overflow: hidden;
    font-size: 10px;
    background-color: #bad8f0;

}
.nav ul{
    margin: 0;
    padding: 0;
}
.nav li{
    list-style: none;
    padding: 10px;
    text-align: center;
    border-bottom: 1px solid #20a0ff
}
.iconfont{
    font-size: 24px;
}
</style>

