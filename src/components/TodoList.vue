<template lang="">
    <section>
        <transition-group name="list" tag=ul>
            <li class="shadow"
            v-for="(todoItem, index) in propsdata"
            :key="todoItem"> 
            <i class="editBtn fa fa-edit"></i>
            {{ todoItem }}

            
                <div class="btn">
                    <span class="checkBtn" disabled type="button" @click="checkTodo(todoItem,index)">
                        <i class="fa fa-check"></i>       
                    </span>                    
                    
                    <span class="removeBtn" type="button" @click="removeTodo(todoItem, index)">
                        <i class="fa fa-trash-alt" ></i>
                    </span>
                </div>
            </li>
        </transition-group>
    </section>
</template>
<script>
export default {
    props:['propsdata'], //반복해야할 대싱이 APP의 배열이기 때문에.
    data(){
        return {

        }
    },  
    methods:{
        checkTodo(todoItem, index){
            console.log("완료버튼")
            this.$emit('checkTodo', todoItem, index)
        },
        removeTodo(todoItem, index){
            console.log("삭제버튼")
            this.$emit('removeTodo', todoItem, index)
        }
    }
}
</script>
<style>
ul{
    list-style-type: none;
    padding-left:0px;
    margin-top:0;
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
    align-items: center 
}
.list-item{
    display: inline-block;
    margin-right: 10px;
}
.list-move{
    transition: transform 1s;
}
.list-enter-active, .list-leave-active{
    transition: all 1s;
}
.list-enter, .list-leave-to{
    opacity: 0;
    transform: translateY(30px)
}

.btn{
    margin-left: auto;
}

.editBtn{
    line-height: 45px;
    color: #ff4c4ca9;
    margin-right: 5px;
}
.checkBtn{
    margin-right: 7.5px;
    color: blue;
}

.removeBtn{
    /* margin-left: auto; */
    color: rgba(93, 93, 93, 0.616);
}
    
</style>