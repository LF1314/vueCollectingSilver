<template>
  <div id="app">
    <Leftnav></Leftnav>
    <div class="main">
       <router-view/>
    </div>
  </div>
</template>

<script>
import Leftnav from './components/Leftnav'
export default {
  name: 'App',
  components:{
    Leftnav

  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: left;
  color: #2c3e50;
  margin-top: 60px;
  background-color: #f2f2f2;
  width: 100%;
  height: 100%;
}
.main{
  width: 95%;
  height: 100%;
  float: left;
  overflow: hidden;

}
</style>
