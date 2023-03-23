<template lang="">
    <div class = "inputBox shadow">
        <input type="text" 
        focus
        v-model.trim="newTodoItem" 
        placeholder="추가 할 내용을 적어주세요."
        @keyup.enter="addTodo"
        />
        <span class="addContainer" @click="addTodo">
            <i class="fas fa-pencil-alt"></i>
        </span>
        
        <todo-modal v-if="showModal" @close="showModal=false">
            <h3 slot="header">경고</h3>
            <span slot="footer" @click="showModal=false">
                내용을 입력하세요.
                <i class="closeModalBtn fas fa-times"></i>
            </span>
        </todo-modal>

    </div>
</template>
<script>
import TodoModal from '@/components/common/TodoModal.vue';
export default {
    components: {
        TodoModal,
    },
    data(){
        return{
            newTodoItem:'',
            showModal: false, 
        }
    },
    methods:{
        addTodo(){
            if(this.newTodoItem !== ''){
                this.$emit('addTodo', this.newTodoItem)
                this.clearInput();
            }else {
                console.log("반응")
                this.showModal = !this.showModal;
            }
        },
        clearInput(){
            this.newTodoItem = ''
        }
    }
}
</script>
<style>
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
    display: inline-block;
    width: 3rem;
    border-radius: 0 5px 5px 0;
}
.addBtn{
    color: white;
    vertical-align: middle;
}
</style>