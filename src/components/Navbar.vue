<template>
    <div>
        <nav class="grey lighten-3 ">
            <ul>
                <li :class="{active:isAll}"><a @click="onApplyFilter('all')">
                        All
                    </a>
                </li>
                <li :class="{active:!isCompleted && !isAll}">
                    <a @click="onApplyFilter('active')">
                        Active
                    </a>
                </li>
                <li :class="{active:isCompleted && !isAll}">
                    <a @click="onApplyFilter('completed')">
                        Completed
                    </a>
                </li>
            </ul>
        </nav>
    </div>
</template>
<script>
export default {
    name: 'Navbar',
    props: ['isAll', 'isCompleted'],
    methods: {
        onApplyFilter(status) {
            this.$emit("eventApplyFilter", status)
        }
    }
}
</script>
<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
ul {
    margin-left: 5%;
}

div {
    padding-bottom: 60px;
}

a {
    color: black;
}

.active a {
    color: darkslategrey;
}
</style>