<template>
    <div class="inputBox shadow">
        <input
            type="text"
            placeholder="할 일을 입력해주세요."
            v-model="newTodoItem"
            v-on:keyup.enter="addTodo"
        />
        <span v-on:click="addTodo" class="inputBtn">
            <i class="fa-solid fa-plus"></i>
        </span>
        <!-- 모달 팝업 설정 -->
        <AlertModal v-if="showModal">
            <h3 slot="header">주의</h3>
            <span slot="footer"
                >할 일을 입력해주세요.
                <i
                    class="closeModalBtn fa-sharp fa-solid fa-square-xmark"
                    v-on:click="showModal = false"
                ></i
            ></span>
        </AlertModal>
    </div>
</template>

<script>
import AlertModal from "./common/AlertModal.vue";
export default {
    data() {
        return { newTodoItem: "", showModal: false };
    },
    methods: {
        addTodo() {
            // console.log("새로입력한 값은?", this.newTodoItem);
            // localStorage.setItem(this.newTodoItem, this.newTodoItem);
            //setItem(키,벨류) : 로컬 스토리지에 데이터를 추가하는 API

            //공백도 입력되는 상황 막아주기 위해
            if (this.newTodoItem !== "") {
                let value = this.newTodoItem && this.newTodoItem.trim();
                // localStorage.setItem(this.newTodoItem, value); 직접 저장하지 않게
                //this.newTodoItem = ""; //분리, 단일책임원칙
                this.$emit("addTodo", value); //상위 App.vue에 addTodo, value 전달
                this.clearInput();
            } else {
                //텍스트 미 입력시 모달 팝업
                this.showModal = true;
            }
        },
        clearInput() {
            //인풋박스 입력 후 초기화
            this.newTodoItem = "";
        },
    },
    components: {
        AlertModal: AlertModal,
    },
};
</script>

<style scoped>
.inputBox {
    background-color: #fff;
    height: 50px;
    line-height: 50px;
    border-radius: 10px;
}
.inputBtn {
    float: right;
    color: #000;
    background: linear-gradient(45deg, darkorange, lemonchiffon);
    width: 50px;
    height: 50px;
    line-height: 50px;
    border: 1px solid #fff;
    box-sizing: border-box;
    border-radius: 0 10px 10px 0;
    cursor: pointer;
}
input {
    border: none;
    font-size: 0.9rem;
    width: calc(90% - 50px);
}
input:placeholder {
    color: #999;
}
input:focus {
    outline: none;
}
h3 {
    font-family: "GmarketSansBold";
    padding: 0;
    margin: 0;
}
i {
    color: cadetblue;
    font-size: 22px;
    line-height: 48px;
    vertical-align: top;
    font-weight: bold;
}
.closeModalBtn {
    color: #000;
    position: absolute;
    bottom: 20px;
    right: 20px;
    width: 20px;
    height: 20px;
    line-height: 20px;
    cursor: pointer;
}
</style>
