<template>
    <div>
        <bro1 @receive='handler'></bro1>
        <bro2 :dat='arr' @recei='handleremove'></bro2>
    </div>
</template>
<script>
import bro1 from "./bro1.vue";
import bro2 from "./bro2.vue";
export default {
    components:{
        bro1,
        bro2
    },
    data(){
        return {
            arr: [
                    {
                        imgSrc: './rjl/10.jpg',
                        proName: "任嘉伦的铠甲",
                        numb:1,
                        id: Math.random().toString(32).substring(2),
                        proPrice: 10,
                        count: 1,
                        val: false
                    },
                    {
                        imgSrc: './rjl/10.jpg',
                        proName: "任嘉伦的头套",
                        numb:2,
                        id:Math.random().toString(32).substring(2),
                        proPrice: 9.9,
                        count: 1,
                        val: false
                    },
                    {
                        imgSrc: './rjl/10.jpg',
                        proName: "任嘉伦的外套",
                        numb:3,
                        id: Math.random().toString(32).substring(2),
                        proPrice: 5,
                        count: 1,
                        val: false

                    }
                ],
                
        }
    },
    methods:{
        handler(input){
            console.log(input);
            this.arr.push(input)
        },
        handleremove(removedat){
            console.log(removedat);
            this.arr=removedat
        }
       
    }
}
</script>
<style>
    * {
        margin: 0;
        padding: 0
    }

    img {
        width: 50px;
        height: 50px;
    }

    #app {
        width: 600px;
        min-height: 200px;

        margin: 100px;
    }

    .head {
        border: 2px solid skyblue;
        margin-bottom: 10px;
        padding: 10px;
    }

    .main {
        border: 2px solid skyblue;
        margin-bottom: 10px;
        padding: 10px;
    }

    table {
        border: 2px solid slateblue;
        width: 100%;
        border-collapse: collapse;
        text-align: center;
    }

    thead {
        color: #fff;
        font-size: 18px;
        font-weight: 800;
        background-color: rgb(47, 110, 173);
    }

    thead>tr>td {
        padding: 4px;
    }

    td {
        border: 2px solid skyblue;
        margin-bottom: 6px;

    }

    button {
        padding: 4px;
    }

    span {
        width: 20px;
        height: 20px;
        background-color: #eee;
        display: inline-block;
    }

    strong {
        margin: 0 4px;
    }

    .mm {
        text-align: center;
    }
</style>


