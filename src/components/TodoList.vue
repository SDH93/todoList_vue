<template>
    <div>
        <TransitionGroup TransitionGroup name="list" tag="ul">
            <!-- vue 2.2.0 이상에서는 key값 필수, propsdata로 파꿈 -->
            <li
                class="shadow"
                v-for="(todoItem, index) in propsdata"
                :key="index"
            >
                <i class="checkBtn fa-solid fa-paper-plane"></i>
                <span class="text">{{ todoItem }}</span>
                <span class="removeBtn" @click="removeTodo(todoItem, index)">
                    <i class="fa-regular fa-trash-can"></i>
                </span>
            </li>
        </TransitionGroup>
    </div>
</template>

<script>
// import gsap from "gsap";

export default {
    props: ["propsdata"],

    /*  App.vue로 이동
    data() {
        return { todoItems: [] }; //로컬스토리지 내용을 집어넣을 배열 선언
    },
    created: function () {
        if (localStorage.length > 0) {
            for (let i = 0; i < localStorage.length; i++) {
                this.todoItems.push(localStorage.key(i));
            }
        }
    },
    */
    methods: {
        removeTodo: function (todoItem, index) {
            // console.log("키 " + index + ", 밸류 " + todoItem);
            this.$emit("removeTodo", todoItem, index);

            /* App.vue로 가져감
            localStorage.removeItem(todoItem); //로컬스토리지에서 삭제
            this.todoItems.splice(index, 1);
            */
            //.splice() : 배열 특정 항목을 제거
        },
        // onBeforeEnter(el) {
        //     el.style.opacity = 0;
        //     el.style.height = 0;
        // },
        // onEnter(el, done) {
        //     gsap.to(el, {
        //         opacity: 1,
        //         height: "50px",
        //         delay: 0,
        //         onComplete: done,
        //     });
        // },
        // onLeave(el, done) {
        //     gsap.to(el, {
        //         opacity: 0,
        //         height: 0,
        //         delay: 0,
        //         onComplete: done,
        //     });
        // },
    },
};
</script>

<style scoped>
ul {
    padding: 0;
    margin: 0;
    min-height: 30px;
}
li {
    background: rgba(255, 255, 255, 0.5);
    display: flex;
    justify-content: flex-start;
    height: 50px;
    line-height: 50px;
    margin: 10px 0;
    list-style: none;
    border-radius: 10px;
    color: #333;
    font-weight: 700;
    text-align: left;
    padding-left: 10px;
    height: 50px;
}
.checkBtn {
    line-height: 50px;
    margin-right: 7px;
    color: coral;
}
.text {
    width: calc(100% - 10px);
    white-space: nowrap;
    overflow: hidden;
    text-overflow: ellipsis;
    /* 말줄임표 적용 */
}
.removeBtn {
    width: 50px;
    height: 50px;
    text-align: center;
    cursor: pointer;
}
.list-move, /* 움직이는 엘리먼트에 트랜지션 적용 */
.list-enter-active,
.list-leave-active {
    transition: all 0.3s ease;
}

.list-enter,
.list-leave-to {
    opacity: 0;
    transform: translateX(30px);
}
</style>
