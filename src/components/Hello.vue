<script setup>
defineProps({
    text: {
        type: String
    }
});
import DisplayCpn from './DisplayCpn.vue';
</script>
<script>
var arra = ['dasd', 'jdjhdj', 'kdkdk']
const arrb = []
export default {
    components: DisplayCpn,
    data() {
        return {
            isEmpty: false,
            text: '',
            text1: '',
            addBtn: true,
            todos: [{
                tieude: '',
                editBtn: false,
                mota: '',
                idDone: false
            }],
        }
    },
    methods: {
        addTodos: function () {
            if (this.text && this.text1) {
                this.todos.push({
                    tieude: this.text,
                    mota: this.text1,
                    editBtn: false,
                    isDone: false
                })
                this.isEmpty = false
                arra = [...this.todos]
                this.text = '',
                    this.text1 = ''
            } else {
                console.log('Khong them vao duoc')
                this.isEmpty = true
            }

        },
        editTodos: function (index) {
            this.text = this.todos[index].tieude
            this.text1 = this.todos[index].mota
            for (let i = 0; i < this.todos.length; i++) {
                this.todos[i].editBtn = false
            }
            this.todos[index].editBtn = true
            this.addBtn = false
        },
        editComplete: function (index) {
            this.todos[index].tieude = this.text
            this.todos[index].mota = this.text1
            this.text = '',
                this.text1 = ''
            this.todos[index].editBtn = false
            this.addBtn = true
        },
        doneTodo: function (index) {
            this.todos[index].isDone = true
            console.log(this.todos[index].isDone)
        }
    }
}
</script>
<template>
    <div class="container">
        <h1>Todo List</h1>
        <div class="todos">
            <h3>Title<br /></h3>
            <input v-model="text" placeholder="edit me" />
            <h3>Description <br /></h3>
            <input v-model="text1" placeholder="edit me" />
            <div>
                <p>Uncompleted</p>
                <li style="list-style-type: none;
                " v-for="(item, index) in todos" :key="index">
                    <div v-if="(!item.isDone) && (item.tieude || item.mota)" class="display">
                        <span>{{ item.tieude }}<br /></span>
                        <span>{{ item.mota }} <br></span>
                        <button v-if="!item.editBtn" v-on:click="todos.splice(index, 1)">Delete</button>
                        <button v-if="!item.editBtn" v-on:click="editTodos(index)">Edit</button>
                        <button v-if="item.editBtn" @click='editComplete(index)'>Ok</button>
                        <button v-if="!item.editBtn" @click='doneTodo(index)'>Done</button>
                    </div>
                </li>
            </div>
            <div>
                <p>Completed</p>
                <li style="list-style-type: none;
                " v-for="(item, index) in todos" :key="index">
                    <div v-if="(item.isDone)" class="display">
                        <span>{{ item.tieude }}<br /></span>
                        <span>{{ item.mota }} <br></span>
                    </div>
                </li>
            </div>
            <span v-if="isEmpty" style="color: red;">Vui long khong de trong<br></span>
            <button v-if="addBtn" v-on:click='addTodos()'>Add</button>
        </div>
    </div>
    <DisplayCpn :todos="arra" />
</template>
<style scoped>
.container {
    width: '100%';
    height: 1000;
    background-color: aliceblue;
    flex-direction: column;
    justify-content: center;
    align-items: center;
}

.input {
    margin: 50;
    background-color: aqua;
}

.display {
    justify-content: center;
    align-items: center;
    /* background-color: blue; */
}
</style>