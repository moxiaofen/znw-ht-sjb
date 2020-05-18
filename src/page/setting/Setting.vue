<template>
  <div class="bg">
      <van-nav-bar
        class="bar"
        title="设置"
        left-arrow
        fixed
        border='false'
        @click-left="$router.back(-1)"
      />
      <ul class="cellBox" >
        <li class="cell" @click="toPage(cell.toKey)" v-for="cell in cellList"  :key='cell.toKey'>
          <img  :src="cell.src" >
          <span > {{cell.title}}</span>
        </li>
      </ul>

  </div>
</template>

<script>
  import { NavBar } from 'vant';

  export default {
    components: {
       [NavBar.name]: NavBar,
    },
    data() {
      return {
          cellList : [
             {
                toKey : 'PersonInfo',
                title : '个人信息设置',
                src : require('../../assets/iv_gerenxinxi.png')
             },
             {
                toKey : 'CompanyInfo',
                title : '企业信息设置',
                src : require('../../assets/iv_qiyexinxi.png')
             }
          ]
      }
    },
    methods: {
      toPage(msg){
         if ('PersonInfo' == msg) {
          this.$router.push({
            path: this.$RM.PersonInfo
          })
        }
        if ('CompanyInfo' == msg) {
          console.log(2)
          this.$router.push({
            path: this.$RM.CompanyInfo
          })
        }
      }
    }
  }
</script>

<style scoped>
@import "../../css/common";
.cellBox {
    margin-top: 46px;
  }
 
</style>
