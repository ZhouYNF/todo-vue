<template>
  <div class="todo-header" >
 
        <div class="todo_he" >添加任务</div>
     	  <!-- 添加键盘事件   并将input的value值 用intext获取 -->
        <a-input class="ainput" placeholder="请输入任务"  size="large"  v-model="title"  @keyup.enter='addItem'>
          <a-icon slot="suffix" type="close-circle" @click="emitEmpty" v-show="title" />
        </a-input>
  </div>
</template>


<script>
    export default {
      props:{
        addTodo:Function
      },
        data(){
          return{
            title:''
          }
        },
      methods: {
          emitEmpty () {
            this.title = ''
          },
          addItem(){
            //1.检查输入的合法性
            const title = this.title.trim()
            if(!title){
              alert('必须输入')
              return
            }
            //2.根据输入生成一个todo对象
            const todo = {
              title,
              complete: false
            }
            //3.添加到todos
            this.addTodo(todo)
            //4.清除输入
            this.title=''
          }
      }
    }
</script>
<style>
.todo_he{
  font-size: 30px;
}
.ainput{
  width: 400px;
}
</style>

