<template>
  <div id="app">
    <TodoHeader></TodoHeader>
    <TodoInput v-on:addTodoItem="addOneItem"></TodoInput>
    <TodoList v-bind:propsdata="todoItems" v-on:removeItem="removeOneItem" v-on:toggleItem="toggleOneItem"></TodoList>
    <TodoFooter v-on:clearAll="clearAllItem"></TodoFooter>
  </div>
</template>
<script>
import TodoHeader from './components/TodoHeader.vue';
import ToInput from './components/TodoInput.vue';
import TodoList from './components/TodoList.vue';
import TodoFooter from './components/TodoFooter.vue';



//상위로 올려서 처리하려고 app.vue 사용
//하위를 사용하는 이유는 재사용을 하기 위해서 ui 표현을 위함
export default {
  data: function(){
    return{
      todoItems: []
    }
  },
  methods:{
    addOneItem:function(todoItem){
      var obj ={completed: false, item: todoItem};
      // 저장하는 로직
      localStorage.setItem(todoItem, JSON.stringify(obj)); //자바스크립트를 스트링으로 변환
      this.todoItems.push(obj);
    },
    removeOneItem:function(todoItem, index){
      localStorage.removeItem(todoItem.item);
      this.todoItems.splice(index, 1); //특정 index에서 하나 지움
    },
    toggleOneItem:function(todoItem, index){
      // todoItem.completed = !todoItem.completed;
      // 동작과는 상관이 없지만 조금 더 명확한 코드
      this.todoItems[index].completed = !this.todoItems[index].completed;
      //로컬 스토리지에 갱신하는 과정
      localStorage.removeItem(todoItem.item); //업데이트가 없기 때문에 삭제하고 다시 만들어 줌
      localStorage.setItem(todoItem.item, JSON.stringify(todoItem));
    },
    clearAllItem:function(){
      localStorage.clear();
      this.todoItems=[];
    }
  },
   created:function(){
        if(localStorage.length>0){
            for(var i =0; i<localStorage.length; i++){
                if(localStorage.key(i) !== 'loglevel:webpack-dev-server'){
                   this.todoItems.push(JSON.parse(localStorage.getItem(localStorage.key(i))));
                }
            }
        }
    },

  components:{
    //컴포넌트 태그명: 컴포넌트 내용
    "TodoHeader": TodoHeader,
    "TodoInput": ToInput,
    "TodoList": TodoList,
    "TodoFooter": TodoFooter
  }
}
</script>
<style>
  body{
    text-align: center;
    background-color: #F6F6F6;
  }
  input{
    border-style: groove;
    width: 200px;
  }
  button{
    border-style: groove;
  }
  .shadow{
    box-shadow: 5px 10px 10px rgba(0, 0, 0, 0.03);
  }
</style>