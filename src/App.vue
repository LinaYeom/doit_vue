<template>
  <div id="app">
    <todo-header></todo-header>
    <todo-input @addTodo="addTodo" @ModalTodo="ModalTodo"></todo-input>
    <todo-list :propsdata="todoItems" @removeTodo="removeTodo" @checkTodo="checkTodo"></todo-list>
    <todo-footer @removeAll="clearAll"></todo-footer>

    <todo-modal v-if="modal.show" @close="modal.show = false">
      <h3 slot="header">{{ this.modal.title }}</h3>
      <span slot="footer" @click="modal.show = false">
        {{ this.modal.content }}
        <i class="closeModalBtn fas fa-times"></i>
      </span>
    </todo-modal>
  </div>
</template>

<script>
import TodoFooter from "./components/TodoFooter.vue";
import TodoHeader from "./components/TodoHeader.vue";
import TodoInput from "./components/TodoInput.vue";
import TodoList from "./components/TodoList.vue";
import TodoModal from "@/components/common/TodoModal.vue";

export default {
  name: "App",
  components: {
    TodoFooter,
    TodoHeader,
    TodoInput,
    TodoList,
    TodoModal,
  },
  data() {
    return {
      todoItems: [], // 데이터를 받아서 처리하기때문에 배열데이터 생성
      modal: {
        show: false,
        title: "",
        content: "",
      },
    };
  },
  created() {
    if (localStorage.length > 0) {
      for (var i = 0; i < localStorage.length; i++) {
        this.todoItems.push(localStorage.key(i));
      }
    }
  },
  methods: {
    addTodo(todoItem) {
      // 전달 받은 값을 담기 위해서
      if (this.todoItems.some((v) => v === todoItem)) {
        this.modal.show = !this.modal.show;
        this.modal.title = "오류";
        this.modal.content = todoItem + "은 중복된 값입니다.";
      } else {
        localStorage.setItem(todoItem, todoItem);
        this.todoItems.push(todoItem);
      }
    },
    ModalTodo() {
      this.modal.show = !this.modal.show;
      this.modal.title = "경고";
      this.modal.content = "입력된 값이 없습니다";
    },
    checkTodo(todoItem, index){
      localStorage.removeItem(todoItem); 
      this.todoItems.splice(index, 1);
      
      this.todoItems.push(todoItem);
      localStorage.setItem(todoItem, todoItem);

    /* 나중에 추가해야할 내용 */
      // let hap = this.todoItems.filter(todoItem => todoItem !== index)      
      // console.log(hap)
      // filer 고유의 키값이 필요하다. 객체배열만들어서 활용... id 값이 추가될때마다 1씩 
      // 고유의 키값 바뀌지 않는 값 오르는 값으로 아이디를 만들어서 배열의 변경 정렬 
    },
    removeTodo(todoItem, index) {
      localStorage.removeItem(todoItem); // 로컬스토리지의 removeItem메소드는 한개의 아이템을 삭제
      this.todoItems.splice(index, 1); //누른 값의 인덱스0 부터 1까지의 값을 복사 -> 그렇기에 클릭한것만 가져온다.
    },
    clearAll() {
      localStorage.clear(); //로컬스토리지 삭제
      this.todoItems = []; // 배열도 같이 비워줌
    },
  },
};
</script>

<style>
body {
  text-align: center;
  background-color: beige;
}

input {
  border-style: groove;
  width: 200px;
}
.shadow {
  box-shadow: 1px 5px 5px rgba(119, 119, 119, 0.3);
}
</style>
