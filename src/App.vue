<template>
  <div class="todo-wrap">
    <TodoHeader :addTodo="addTodo"/>
    <TodoList :todos="todos" :deleteTodo="deleteTodo" :whichShow="whichShow" :defaultShow="defaultShow" />
    <TodoFooter :todos="todos" :deleteCompeteTodos="deleteCompeteTodos"   :selectAllTodos="selectAllTodos" :switchStatus="switchStatus" :dataStatus="dataStatus" :dataStatusIndex="dataStatusIndex"/>
  </div>
</template>

<script>
  import TodoHeader from './components/TodoHeader'
  import TodoList from './components/TodoList'
  import TodoFooter from './components/TodoFooter'
export default {
    name:"App",
    data() {
      return{
			      todos:[
              {title:'asd',complete:false},
              {title:'dsf',complete:true},
              {title:'zczxc',complete:false},
            ],
            dataStatus: ["All", "Active", "Completed"],
            dataStatusIndex: 0,
            whichShow: true,
            defaultShow: true
      }
    },
    components:{
      TodoHeader,
      TodoList,
      TodoFooter
    },
    methods:{
      //添加
      addTodo(todo){
        this.todos.unshift(todo)
      },
      //删除
      deleteTodo(index){
        this.todos.splice(index,1)
      },
      //删除所有选中的todo
      deleteCompeteTodos(){
        //过滤出false的留下 todo.complete取反
        this.todos = this.todos.filter(todo=>!todo.complete)
      },
      //全选/全不选
      selectAllTodos(check){
        this.todos.forEach(todo => todo.complete = check)
      },
      //三种状态
      switchStatus(index) { //通过if条件判断操作
        this.dataStatusIndex = index
        if (this.dataStatus[index] === "Active") {
            this.defaultShow = false
            this.whichShow = false
        } else if (this.dataStatus[index] === "Completed") {
            this.defaultShow = false
            this.whichShow = true
        } else if (this.dataStatus[index] === "All") {
            this.defaultShow = true
        }
      }
    }
}
</script>
<style>
.todo-wrap {
        width: 800px;
        height: 900px;
        margin: 0 auto;
        text-align: center;
        background-color: rgb(245, 245, 245);
        padding: 24px 0;
    }
</style>
