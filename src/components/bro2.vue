<template id="bro2">
        <div>
        <table>
            <thead>
                <tr>
                    <td>
                        全选<input type="checkbox" v-model=identity  @click="allchecked">
                        反选<input type="checkbox"  @click='returnchoice'>
                    </td>
                    <td>产品图片</td>
                    <td>编号</td>
                    <td>品牌名称</td>
                    <td>价格</td>
                    <td>数量</td>
                    <td>操作</td>
                </tr>
            </thead>
            <tbody>
                <tr v-for="(item,index) in dat" :key="item.id">
                    <td><input type="checkbox" v-model='choice' :value='item' @click="loglechecked"></td>
                    <td><img src="./rjl/5.jpg"></td>
                    <td>{{item.numb}}</td>
                    <td>{{item.proName}}</td>
                    <td>{{item.proPrice}}</td>
                    <td>
                        <button @click='reducecount(item)' v-dis:[item.count]>&nbsp; -&nbsp;</button>
                        <strong>{{item.count}}</strong>
                        <button @click='addcount(item)'>&nbsp;+&nbsp;</button>
                    </td>
                    <td><button @click="remove(item)">删除</button></td>
                </tr>
            </tbody>
            <tfoot>
                <tr>
                    <th style=" border:2px solid skyblue;">总价</th>
                    <th colspan="6">{{totalprice}} </th>
                    <!-- -->
                </tr>
            </tfoot>
        </table>
        <div class="mm" v-show=flag>没有更多数据了</div>
    </div>
</template>
<script>

export default{
    props:['dat'],

    data(){
        return{
           choice:[],
           totalprice:'0',
           flag:false,
           identity:false,
           signs:false,
        }
    },
    methods:{
        //数量加
        addcount(item){
            item.count++
        },
        //数量减
        reducecount(item){
            item.count--
        },
        remove(item){
            //利用filter方法删除掉和当前删除的数据id相等的数据
            
           let removedat= this.dat.filter((datid)=>{
                return datid.id!==item.id
            })
            this.$emit("recei",removedat)
            //通过判断数据长度来控制.mm的显示隐藏
            if(this.dat.length===1){
                this.flag=true
            }else{
                this.flag=false
            }
            console.log(this.flag);
        },
        //实现全选功能
        allchecked(){
             if(this.identity===false){
                this.choice=this.dat
            }else if(this.identity===true){
                this.choice=[]
            }
            //   console.log(this.identity);
        },
        //实现下面全选择，全选按钮也会亮
        loglechecked(){
            console.log(this.choice.length,this.dat.length);
            //为甚么choice的length要加1，因为每次点击就立刻把choice的length传过来了，还没来得及把数据放到choice中
             if(this.choice.length+1===this.dat.length){
                this.identity=true
            }else{this.identity=false}
            console.log(this.identity);
        },
        returnchoice(){
            this.choice=this.dat.filter((item)=>{
                return this.choice.indexOf(item)==-1
            })
        }
    },
    //写一个监听函数，监听数据的变化，实现总价计算
    watch:{
        choice:{
            handler(newVal,oldVal){
            // console.log("newVal",newVal);
            // console.log("oldVal",oldVal);
            let sum=0
            newVal.forEach(item => {
                sum+=((item.count-0)*100)*((item.proPrice-0)*100)/10000
            });
            this.totalprice=sum

        },
        immediate: true,
        deep:true
        }
    },
    //计算属性,监听数据的变化，实现总价计算
    // computed:{
    //     totalprice(){
            
    //         let sum= this.choice.reduce(function(pre,item){
    //             // console.log(item.count,);
    //            pre= pre + ((((item.count)*100*(item.proPrice)*100)/10000).toFixed(2)-0)
    //            return pre
    //         },0)
    //         console.log(sum);
    //         return sum
    //     }
    // },
    // 设置一个自定义指令，获取数量加减的元素节点
    directives:{
       dis:{
        inserted(el,binding){
              if(binding.arg==1){
                el.disabled=true
            }
        },
         update(el,binding){
            // console.log(binding.arg);
            if(binding.arg==1){
                el.disabled=true
            }else{el.disabled=false}
        }
       }
    }

}
</script>

   