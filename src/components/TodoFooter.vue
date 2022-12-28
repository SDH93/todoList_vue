<template>
    <div class="clearAllWrap">
        <span v-on:click="clearTodo" class="clearAllBtn">Clear All</span>
    </div>
</template>

<script>
export default {
    methods: {
        clearTodo() {
            this.$emit("removeAll");
        },
    },
};
</script>

<style scoped>
.clearAllWrap {
    background-color: lemonchiffon;
    line-height: 50px;
    width: 150px;
    margin: 10px auto;
    border-radius: 10px;
}
.clearAllBtn {
    color: #333;
    font-family: "GmarketSansBold", sans-serif;
    cursor: pointer;
    display: block;
}
</style>
