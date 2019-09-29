<template>
    <div class="collection-item left-align row" :class="{ done: isDone}">
        <label :for="idComputed">
            <input type="checkbox" class="filled-in" :id="idComputed" @change="onTaskStatusChange" :checked="isDone">
            <span>
                {{ text }}
            </span>
        </label>
        <div class="secondary-content">
            <i class="material-icons right-align clickable" @click="onTaskDelete">delete</i>
        </div>
    </div>
</template>
<script>
export default {
    name: "ListItem",
    props: {
        id: {
            type: Number,
            default: 0
        },
        text: {
            type: String,
            default: ""
        },
        isDone: {
            type: Boolean,
            default: false
        }
    },
    computed: {
        idComputed() {
            return `item-${this.id}`
        }
    },
    methods: {
        onTaskStatusChange(e) {
            const checked = e.target.checked
            this.$emit("eventTaskStatusChange", this.id, checked)
        },
        onTaskDelete(e) {
            this.$emit("eventTaskDelete", this.id)
        }
    }
}
</script>
<style>
.done span {
    text-decoration: line-through;
    color: darkgrey;
}

.done.collection-item.row {
    background-color: #f0f0f0;
}

.done i {
    color: #66ccbb;
}

.clickable {
    cursor: pointer;
}

.span {
    word-wrap: break-word;
}
</style>