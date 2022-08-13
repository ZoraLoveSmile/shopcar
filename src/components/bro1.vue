<!-- bro1 -->
<template id="bro1">
  <div>
    <div class="head">
      编号：<input type="text" v-model="numb" />品牌名称：<input
        type="text"
        v-model="proName"
      />
      <br />
      产品图片地址：<input type="text" v-model="imgSrc" />价格：<input
        type="text"
        v-model="proPrice"
      />
      <button @click="send">添加</button>
    </div>
    <div class="main">品牌名称:<input placeholder="请输入搜索条件" /></div>
  </div>
</template>
<script>
export default{
    data(){
        return {
            proName:"",
            numb:"",             
            imgSrc:"",
            proPrice:"",
          
        }
    },
    methods:{
        send(){
           
            if(!this.proName||!this.numb||!this.imgSrc||!this.proPrice){
                return
            }
            let obj={
            proName:this.proName,
            numb:this.numb,
            id: Math.random().toString(32).substring(2),
            imgSrc:this.imgSrc,
            proPrice:this.proPrice,
            count: 1,
            val: false,
        }
            this.$emit("receive",obj)
            //清空数据框
            this.proName="",
            this.numb="",             
            this.imgSrc="",
            this.proPrice=""
        },
        
    }
}
</script>