<template>
  <div>
    <mt-header title="热门推荐" fixed style="background:#c63b2d;"></mt-header>
    <p class='rm'>每日推荐></p>
    <ul>
      <li v-for='(item,i) of rmsinglist' :key='i'>
        <img :src="item.picUrl" alt="" @click="gosongsdetail(item.id)">
        <p>{{item.name}}</p>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  data(){
    return{
      rmsinglist:[]
    }
  },
  methods:{
    loadmore(){
      var singListUrl='http://music.apiopen.top/personalized'
      fetch(singListUrl)
      .then(res=>{
        return res.json()
      })
      .then(result=>{
        this.rmsinglist=result.result
      })
      .catch(err=>{console.log(err)})
    },
    gosongsdetail(e){
      this.$router.push({name:'gd',params:{gd:e}})
    }
  },
  created(){
   this.loadmore()
 }
}
</script>

<style scoped>
  div,p,ul{padding:0 ;margin: 0;}
  div{
    margin-bottom:60px;
    margin-top:50px
  }
  ul{
    display:flex;
    width: 100%;
    flex-wrap:wrap;
  }
  ul li{
    list-style: none;
    flex: 30%;
    padding:5px
  }
  ul li img{
    width:120px;
    border-radius:3px
  }
  ul li p{
    font-size:14px;
    
  }
  .hd{
    width:100%;height:50px;
    border: none
  }
  .rm{
    font-size:22px;
    color:#c63b2d;
    padding:5px;
    border-bottom:1px solid #c63b2d
  }
  input{
    width:99%;
    height: 30px;
    outline: none;
  }
</style>