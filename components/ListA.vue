<template>
  <div class="row">
      <div class="card" v-for="user in dataObj.users" :key="user.login">
        <a :href="user.html_url" target="_blank">
          <img :src="user.avatar_url" style='width: 100px'/>
        </a>
        <p class="card-text">{{user.login}}</p>
      </div>
        <h1 v-show="dataObj.isFrist">欢迎使用</h1>
        <h1 v-show="dataObj.isLoading">正在加载...</h1>
        <h1 v-show="dataObj.errMsg">{{dataObj.errMsg}}</h1>
    </div>
</template>

<script>
export default {
    name:"ListA",
    data(){
        return {
            dataObj:{
                isFrist:true,
                isLoading:false,
                errMsg:"",
                users:[]
            }
        }
    },
    mounted(){
        //调用时带的参数会传递到形参dataObj
        this.$bus.$on('sendData',(dataObj)=>{
            this.dataObj={...this.dataObj,...dataObj}
        })
    }
}
</script>

<style lang="css" scoped>
.album {
  min-height: 50rem; /* Can be removed; just added for demo purposes */
  padding-top: 3rem;
  padding-bottom: 3rem;
  background-color: #f7f7f7;
}

.card {
  float: left;
  width: 33.333%;
  padding: .75rem;
  margin-bottom: 2rem;
  border: 1px solid #efefef;
  text-align: center;
}

.card > img {
  margin-bottom: .75rem;
  border-radius: 100px;
}

.card-text {
  font-size: 85%;
}

</style>