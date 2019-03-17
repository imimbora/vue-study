<template>
    <div>
        <ul>
            <li v-for="(todo,idx) in todosData" 
                :key="idx"
                :class="{todo:true, complete:todo.isDone, editing: idx === edit.index}">
                <div class="view">
                    <input type="checkbox" :checked="todo.isDone" @click="checkon(todo.date)" class="chk">
                    <label @dblclick="editon(idx, todo.text)">{{todo.text}}</label>
                    <button @click="removeon(todo.date)">삭제</button>
                </div>
                <input type="text" @keypress="submiton" :value="edit.text" class="edit-input">
            </li>
        </ul>
    </div>
</template>

<script>
export default {
    props: {
        todosData: { type: Array, default: () => []},
        edit: {type: Object, defailt: () => {}}
    },
    methods:{
        removeon(date){
            this.$emit("removeTodo",date)
        },
        editon(editonIdx, text){
            alert( (editonIdx+1) + "번째 글 더블클릭! 기존 내용 : " + text)
            this.$emit("setEdit",editonIdx,text)
        },
        submiton({ keyCode, target:{value} }){
            if(keyCode === 13){
                alert("엔터쾅! 새로운 내용 : " + value)
                this.$emit("editTodo",value)
            }
        },
        checkon(date){
            alert('체키라웃')
            this.$emit("toggleIsDone", date)
        }
    }
}
</script>

<style scoped>
input {height:30px; padding:1px 10px;}
button {height:36px; margin-left:20px;}
li {list-style:none;}
li + li {margin-top:10px;}
li.complete {text-decoration:line-through;}
.edit-input {display:none;}
.editing .view {display:none;}
.editing .edit-input {display:inline-block;}
.chk {vertical-align:middle; width:20px; height:20px; margin-right:10px;}
</style>