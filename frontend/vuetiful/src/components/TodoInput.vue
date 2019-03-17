<template>
    <div class="todo-input">
        <input type="text" 
            v-model="todoText" 
            @keypress="handleInput"
            autofocus=""
            placeholder="뭐 해야 하지 ?">
        <button @click="addTodo">추가</button>
    </div>
</template>

<script>
export default {
    data(){
        return{
            todoText: ''
        }
    },
    methods: {
        addTodo(){
            this.$emit("addTodo",this.todoText);
            this.removeTxt();
        },
        handleInput({keyCode, target: {value}}){
            if(keyCode === 13) {
                this.$emit("addTodo",value)
                this.removeTxt();
            }
        },
        removeTxt(){
            this.todoText = ''
        }
    }
}
</script>

<style scoped>
.todo-input {margin-top:30px;}
input {height:30px; vertical-align:middle; padding:1px 10px;}
button {height:36px; vertical-align:middle; margin-left:5px;}
</style>