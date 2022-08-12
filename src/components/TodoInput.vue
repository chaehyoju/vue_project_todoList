<template>
    <div class="shadow inputBox">
        <input type="text" v-model="newTodoItem" v-on:keyup.enter="addTodo">
        <span class="addContainer" v-on:click="addTodo">
            +
        </span>

        <!-- <Modal v-if="showModal" @close="showModal = false">
            <h3 slot="header">경고</h3>
        </Modal> -->
        <Modal v-if="showModal" @close="showModal = true">
            <template v-slot:header>
                <h3>경고</h3>
            </template>
        </Modal>
    </div>
</template>
<script>
import Modal from "./common/ModalForm.vue";

export default {

    data: function(){
        return{
            newTodoItem: "",
            showModal: false
        }
    },
    methods:{
        addTodo: function(){
            if(this.newTodoItem !==''){
                // this.$emit('이벤트 이름', 인자1, 인자2...);
                this.$emit('addTodoItem', this.newTodoItem);
                this.clearInput();
            }
            else{
                //true, false 변환
                this.showModal=!this.showModal;
            }
        },
        clearInput: function(){
            this.newTodoItem='';
        },
        components:{
            Modal: Modal
        }
    }
}
</script>
<style scoped>
input:focus{
    outline: none;
}
.inputBox{
    background: white;
    height: 50px;
    line-height: 50px;
    border-radius: 5px;
}
.inputBox input{
    border-style: none;
    font-size: 0.9rem;
}
.addContainer{
    float: right;
    background: linear-gradient(to right, #6478FB, #8763FB);
    display: block;
    width: 3rem;
    border-radius: 0 5px 5px 0;
}
.attBtn{
    color: white;
    vertical-align: middle;
}
</style>