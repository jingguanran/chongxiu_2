<template>
  <div id="app">

<el-menu
  :default-active="activeIndex2"
  class="el-menu-demo"
  mode="horizontal"
  @select="handleSelect"
  background-color="#545c64"
  text-color="#fff"
  active-text-color="#ffd04b">
  <el-menu-item index="1"><router-link to="/">index</router-link></el-menu-item>
  <el-menu-item index="2"><router-link to="/1">1705b</router-link></el-menu-item>
    <el-menu-item index="3"><router-link to="/2">待重修</router-link></el-menu-item>
      <el-menu-item index="4">已重修</el-menu-item>
 
  </el-menu>

    <router-view/>
  </div>
</template>
<script>
  export default {
    created(){
      if(this.$route.params.state==null){
        this.activeIndex2="1"
      }else{
        this.activeIndex2=parseInt(this.$route.params.state)+1+""
      }
    },
    data() {
      return {
        activeIndex2: ""
      };
    },
    methods: {
      handleSelect(key, keyPath) {
        console.log(key, keyPath);
      }
    }
  }
</script>
<style>
.el-menu-item{
  padding:0
}
a{display:block;padding:0 20px}
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  
  color: #2c3e50;
}
#nav {
  padding: 30px;
}

#nav a {
  font-weight: bold;
  color: #2c3e50;
}

#nav a.router-link-exact-active {
  color: #42b983;
}
</style>
