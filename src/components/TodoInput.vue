<template>
    <div class ="inputBox shadow">
        <input type="text" v-model="newTodoItem" @keyup.enter="addTodo">
        <span class="addContainer" @click="addTodo">
            <i aria-hidden="true" class="addBtn fa fa-plus" ></i>
        </span>
    </div>
</template>

<script>
export default {
    data: function () {
        return {
            newTodoItem: "" //two-way binding
        }
    },
    methods: {
        addTodo: function () {
            if(this.newTodoItem !== ''){
                var obj = {completed: false, item: this.newTodoItem};
                // JSON.stringify -> 객체를 string으로 변환 
                localStorage.setItem(this.newTodoItem, JSON.stringify(obj));
                this.clearInput();
            }
        },
        clearInput: function () {
            this.newTodoItem = '';
        }
    
    }
}
</script>

<style scoped>
input:focus{
  outline:none;
}

.inputBox {
    background: #fff;
    height: 50px;
    line-height: 50px;
    border-radius: 5px;
}

.inputBox input {
    border-style: none;
    font-size: .9rem;
}

.addContainer {
    float: right;
    background: linear-gradient(90deg,#6478fb,#8763fb);
    display: block;
    width: 3rem;
    border-radius: 0 5px 5px 0;
}

.addBtn {
    color: #fff;
    vertical-align: middle;
}

</style>