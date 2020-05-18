<template>
<div>
 
    <div class='cont-sides'>
        <p class="cont-item">回款信息      
        </p>
    </div>
    <ul class="bgcf">
      <li v-for="(item,index) in repaymentList" :key='index' @click="toDetail(item)">
        <div class="receivables-lib">
            <div class=" item-receivables-line1">
              <div>
                <p class="receivables-name ell2 word-break">{{item.paymentNo}}</p>
                <p class="receivables-no">{{item.loanAmt}}</p>
              </div>
            </div>

            <div class="item-receivables-line2">
              <span class="receivables-amount">{{item.loanDate}}</span>
            </div>
            <div class="item-receivables-line3">
              <!-- <span class="receivables-data">{{formatDay(item.paymentEndDate)}}</span> -->
              <span class="receivables-data">{{item.paymentEndDate}}</span>
            </div>
        </div>
      </li>
    </ul>
    <div v-if='tipRepayment' class="tip">暂无更多数据</div>

</div>
</template>

<script>
  // import Divider from '@/components/Divider.vue'
    export default {
        components: {
         // Divider,
        },
        props:['repaymentList','tipRepayment'],
        computed: {},
        data() {
          return {


          }
        },
        created() {
        
        },
        methods: {

          toDetail(item) {
            //this.$store.repaymentItem = item
            //this.$store.commit('setRepaymentItem',item)
            sessionStorage.setItem('repaymentItem',JSON.stringify(item))
            this.$router.push({
              path: this.$RM.LedgerRepayment    
            })
          },
         
          formatDay(num){
            if(num){
                var fnum = ''+num.slice(0,4)+'-'+num.slice(4,6)+'-'+num.slice(6,8)
                return fnum;
            }
          }

        }
    }
</script>

<style scoped>

@import "../../css/common";

</style>
