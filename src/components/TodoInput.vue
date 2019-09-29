<template>
    <form @submit="onAddNewTask">
        <input type="text" placeholder="What needs to be done?" v-model="text" required>
    </form>
</template>
<script>
export default {
    name: "TodoInput",
    data() {
        return {
            text: ""
        }
    },
    methods: {
        onAddNewTask(e) {
            e.preventDefault()
            const taskName = this.text
            this.$emit("eventAddNewTask", taskName)
            this.text = ""
        }
    }
}
</script>