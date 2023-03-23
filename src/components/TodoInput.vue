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
        
    </div>
</template>
<script>

export default {
    components: {
    },
    data(){
        return{
            newTodoItem:'',
        }
    },
    methods:{
        addTodo(){
            if(this.newTodoItem !== ''){
                this.$emit('addTodo', this.newTodoItem)
                this.clearInput();
            }else {
                this.$emit('ModalTodo')
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