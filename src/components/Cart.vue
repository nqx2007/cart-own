<template>
    <div>
        <h2>购物车</h2>
        <table>
            <tr>
                <th>勾选</th>
                <th>课程名称</th>
                <th>课程价格</th>
                <th>数量</th>
                <th>价格</th>
            </tr>
            <tr v-for="(item,index) in courseItem" :key="item.id">
                <td><input type="checkbox" v-model="item.isActive"></td>
                <td>{{item.name}}</td>
                <td>{{item.price}}</td>
                <td><button @click="minus(index)">-</button>{{item.num}}<button @click="add(index)">+</button></td>
                <td>{{item.price*item.num}}</td>
            </tr>
            <tr>
                <td colspan="2">{{isActiveCourse}}/{{allCourse}}</td>
                <td colspan="2">{{allPrice}}</td>
            </tr>
        </table>
    </div>
</template>
<script>
    export default {
        props:['courseItem'],
        methods:{
            minus:function(index){
                let number=this.courseItem[index].num;
                if(number>1){
                    this.$emit("minusNum",index)
                }else{
                    if(window.confirm("sure to delete?")){
                        this.$emit("removeItem",index)
                    }
                }
            },
            add:function(index){
                this.$emit("addNum",index)
            }
        },
        computed:{
            isActiveCourse(){
                return this.courseItem.filter(value=>value.isActive).length
            },
            allCourse(){
                return this.courseItem.length
            },
            allPrice(){
                let num=0;
                this.courseItem.forEach(item=>{
                    if(item.isActive){
                        num+=item.price*item.num
                    }
                })
                return num;
            }

        }

    }
</script>
<style>

</style>