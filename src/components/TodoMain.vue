<template>
    <div>
        <Navbar :isAll="isAll" :isCompleted="isCompleted" @eventApplyFilter="onApplyFilter" />
        <div class="container">
            <TodoInput @eventAddNewTask="onAddNewTask" />
            <div class="collection" v-show="itemList.length">
                <ListItem v-for="item in filteredItemList" :key="item.id" :text="item.text" :id="item.id" :isDone="item.isDone" @eventTaskStatusChange="onTaskStatusChange" @eventTaskDelete="onTaskDelete" />
            </div>
        </div>
    </div>
</template>
<script>
import Navbar from "./Navbar.vue"
import TodoInput from "./TodoInput.vue"
import ListItem from "./ListItem.vue"
export default {
    name: "home",
    components: {
        TodoInput,
        ListItem,
        Navbar

    },
    data() {
        return {
            itemList: [],
            isCompleted: true,
            isAll: true
        }
    },
    computed: {
        filteredItemList() {
            return this.itemList.filter(item => (item.isDone == this.isCompleted || this.isAll))
        }
    },
    methods: {
        onAddNewTask(taskName) {
            const task = {
                id: (new Date()).getTime(),
                text: taskName,
                isDone: false
            }
            this.itemList.unshift(task)
        },
        onTaskStatusChange(id, checked) {
            console.log(id, checked)
            let item = this.itemList.find(i => i.id == id)
            if (item) {
                item.isDone = checked
            }

            console.log(this.itemList)
        },
        onTaskDelete(id) {
            console.log(id)
            let index = this.itemList.findIndex(i => i.id == id)
            if (index > -1) {
                this.itemList.splice(index, 1)
            }
            console.log(this.itemList)
        },
        onApplyFilter(status) {
            if (status == 'all') {
                this.isAll = true
            }
            if (status == 'active') {
                this.isCompleted = false
                this.isAll = false
            }
            if (status == 'completed') {
                this.isCompleted = true
                this.isAll = false
            }
        },
        loadItemList() {
            this.itemList = JSON.parse(localStorage.getItem("VueTodoItems")) || []
            console.log("this.itemList =", this.itemList)
        },
        updateItemList() {
            localStorage.setItem("VueTodoItems", JSON.stringify(this.itemList))
        }

    },
    mounted() {
        this.loadItemList()

    },
    watch: {
        itemList: {
            handler(value) {
                console.log("item changed")
                this.updateItemList()
            },
            deep: true
        }
    },

}
</script>
<style>
.collection {
    border: 0px;
}
</style>