<template>
    <div>
        <transition-group name="list" tag="ul">
            <li v-for="(todoItem, index) in propsdata" v-bind:key="todoItem.item" class="shadow">
            <span class="checkBtn" v-bind:class="{checkBtnCompleted: todoItem.completed}" v-on:click="toggleComplete(todoItem, index)">체크</span>
            <span v-bind:class="{textCompleted: todoItem.completed}">{{todoItem.item}}</span>
            <span class="removeBtn" v-on:click="removeTodo(todoItem, index)">
                삭제
            </span>
            </li>
        </transition-group>
    </div>
</template>
<script>

export default {
    props:['propsdata'],
    methods:{
        removeTodo: function(todoItem, index){
            this.$emit('removeItem', todoItem, index);
        },
        toggleComplete: function(todoItem, index){
            this.$emit('toggleItem', todoItem, index);
        }
    },
}
</script>
<style scoped>
    ul{
        list-style-type: none;
        padding-left: 0px;
        margin-top: 0;
        text-align: left;
    }
    li{
        display: flex;
        min-height: 50px;
        height: 50px;
        line-height: 50px;
        margin: 0.5rem 0;
        padding: 0 0.9rem;
        background: white;
        border-radius: 5px;
    }
    .checkBtn{
        line-height: 45px;
        color: #62acde;
        margin-right: 5px;
    }
    .checkBtnCompleted{
        color: #b3adad;
    } 
    .textCompleted{
        text-decoration: line-through;
        color: #b3adad;
    }
    .removeBtn{
        margin-left: auto;
        color: #de4343;
    }
    /* 리스트 아이템 트랜지션 효과
    vue2는 list-enter를 사용하지만 vue3는 from을 붙여 줘야 됨 문법이 다름
    */
    .list-enter-active,
    .list-leave-active {
        transition: all 1s;
    }
    .list-enter-from,
    .list-leave-to /* .list-leave-active below version 2.1.8 */ {
        opacity: 0;
        transform: translateY(30px);
    }
</style>