<template>
  <div id="app">
      <navigation  v-bind:inshow="seal.inshow" :head_name="seal.head_name"  :right_inshow="seal.right_inshow" :right_name="seal.right_name"></navigation>
         <div @click="route('/me',{'id':1,'name':'liyunlong'})">
            {{name}}
         </div>
      <HelloWorld v-bind:idx="seal.idx"></HelloWorld>
  </div>
</template>
<script>
import HelloWorld from '../views/HelloWorld'
import navigation from '../views/navigation'
export default {
  name: 'App',
  data(){
    return{
      seal:{
          idx:0,
          inshow:true,
          head_name:"哈哈哈",
          right_inshow:true,
          right_name:"djhfwerf"
      } ,
      name:""
    }
  },
 components:{
    HelloWorld,
    navigation,
  },
  methods:{
    route(name,object){

       this.$router.push({ path: name, query: object });
    }
  },
  created(){
    console.log(window.g.baseUrl)
     var that = this;
      that.$axios({
        method: "post",
        url: window.g.baseUrl + "api/Branch/branch_honor",
        params: { 
          shop_id:3,
          p:that.current,
          count:9
        }
      }).then((res)=> {
        console.log(res.data.data.cat_name);
        that.name=res.data.data.cat_name
      });
  }
}
</script>
<style scoped>

</style>
