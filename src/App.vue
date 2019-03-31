<template>
  <div id="app">
    <h1>{{title}}</h1>
    <hr />
    <div>
      <h2>添加课程</h2>
      <div>
        <label for="">课程名称：</label>
        <input type="text" v-model="courseInfo.name">
      </div>
      <div>
        <label for="">课程价格：</label>
        <input type="text" v-model="courseInfo.price">
      </div>
      <div><button @click="addCourseToList">添加课程到列表</button></div>
    </div>
    <div>
      <h2>课程列表</h2>
      <table>
        <tr>
          <th>课程名称</th>
          <th>课程价格</th>
          <th>操作</th>
        </tr>
        <tr v-for="(item,index) in courseList" :key="item.id">
          <td>{{item.name}}</td>
          <td>{{item.price}}</td>
          <td><button @click="addCourseToCart(index)">添加到购物车</button></td>
        </tr>
      </table>
    </div>
    <cart :courseItem="courseItem" @removeItem="remove" @minusNum="minus" @addNum="add"></cart>
  </div>
</template>

<script>
import Cart from './components/Cart.vue'

export default {
  name: 'app',
  components: {
    Cart
  },
  data(){
    return {
        title:'开课吧购物车',
        courseList:[
            {id:1,name:"web全栈开发架构师",price:9998},
            {id:2,name:"python人工智能",price:8888}
        ],
        courseInfo:{
            name:'',
            price:''
        },
        courseItem:[]
    }
  },
  methods:{
      addCourseToList:function(){
          this.courseList.push(this.courseInfo)
      },
      addCourseToCart:function(index){
          let item=this.courseList[index];
          let isHasCourse=this.courseItem.find(value=>value.id===item.id);
          if(isHasCourse){
              isHasCourse.num+=1;
          }else{
              this.courseItem.push({
                  ...item,
                  num:1,
                  isActive:true
              })
          }
      },
      remove:function(index){
          this.courseItem.splice(index,1)
      },
      minus:function(index){
          this.courseItem[index].num-=1;
      },
      add:function(index){
          this.courseItem[index].num+=1;
      }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
