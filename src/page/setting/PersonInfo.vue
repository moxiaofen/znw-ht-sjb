<template>
  <div>
    <van-nav-bar
      class="bar"
      title="个人信息"
      left-arrow
      fixed
      border='false'
      @click-left="$router.back(-1)"
    />

    <van-cell-group class="content">
      <van-cell  title="头像">  
        <!-- <form ref="upload" enctype="multipart/form-data" method="post">         
           <img class="head-img" style="" ref='img' alt="handleFile" :src="src" />
           <input type="file" accept="image/*" class="van-uploader__input input-file" ref="inputImg" @change="handleFile">
        </form> -->
        <img class="head-img" style="" ref='img' alt="handleFile" :src="src" />
        <input type="file" accept="image/*" class="van-uploader__input input-file" ref="inputImg" @change="handleFile">
      </van-cell>

      <van-cell title="用户昵称" is-link :value="loginid"  to="/setting/PersonInfoName" />
      <van-cell title="登录密码" is-link :value="password"  to="/setting/PersonInfoPsw" />
      <van-cell title="绑定邮箱" is-link :value="email"  to="/setting/PersonInfoEmail" />
      <van-cell title="绑定手机" is-link :value="mobile"  to="/setting/PersonInfoPhone" />

    </van-cell-group>

  </div>
</template>

<script>
  import { NavBar , Cell, CellGroup } from 'vant';

  export default {
    components: {
        [NavBar.name]: NavBar,
        [Cell.name]: Cell,
        [CellGroup.name]: CellGroup,
    },
    computed: {},
    data() {
      return {
        nonet: false, //断网
        src: require('../../assets/head.png'),

        //loginSession:{},
        loginid:'',
        mobile:'',
        email:'',
        password:'******'
      }
    },
    created(){
       //this.loginSession = JSON.parse(sessionStorage.getItem('loginSession'))
       if(!sessionStorage.getItem('loginid')){
            this.password=''
       }
       this.loginid = sessionStorage.getItem('loginid')
       this.mobile = sessionStorage.getItem('mobile')
       this.email = sessionStorage.getItem('email')

    },
    methods: {

      handle() {
            // const file = this.$refs.inputImg.files[0];
            // // createObjectURL传入File类型的数据创建url，可以在浏览器看到网络请求
            // const ObjectURL = URL.createObjectURL(file);
            // const rimg = this.$refs.img;
            // rimg.src = ObjectURL;
            // rimg.onload = function(img) {
            //     URL.revokeObjectURL(this.src);  // 释放createObjectURL创建的对象##
            // }
            // var file = document.querySelector("#file").files[0];
            // //创建formdata对象
            // var formdata = new FormData();
            // formdata.append("file",file);
            
      },

      handleFile(){
           //头像未完成
          //  this.handle();
          //  const url = this.$api.ROOT + this.$Constants.CHANGE_HEADERIMG;
          //  this.$http.post(url,{'userId':sessionStorage.getItem('userId')})
          //  .then(function (res) {
          //     //  const data = JSON.parse(res.data);
          //     //  const records = data.records
          //      console.log(res)                           
          // }).catch(function () {
          //    this.$toast(this.$ERRCODE.STATIC_ERRORCDDE.EXCEPTION);
          // })

            let config = {
              headers: {
                'Content-Type': 'multipart/form-data'
              }
            }
            var fileObj = this.$refs.inputImg.files[0];
            var formData = new FormData(); 
            formData.append("file", fileObj);
            console.log(formData)
            const url = this.$api.ROOT + this.$Constants.CHANGE_HEADERIMG;
            this.$http.post(url,formData,config)
            .then(function (res) {
                //  const data = JSON.parse(res.data);
                //  const records = data.records
                console.log(res)                           
            }).catch(function () {
              this.$toast(this.$ERRCODE.STATIC_ERRORCDDE.EXCEPTION);
            })

      }


    },
 

  }
</script>

<style scoped>
.content {
  margin-top: 46px;
  position: relative;
}
.input-right{
  text-align: right;
} 
.bar {
  background-color: #FFC600;
  color: #ffffff;
}
.head-img{
  width:60px;
  height:60px;
  border-radius: 50%;
}
.input-file{
    position: absolute;
    right: 0;
    top: 0;
    height: 100px;
    opacity: 0;
}


</style>
