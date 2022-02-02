<template>
    <div>
        <task-item v-for="t in tasks" :key="t.id" :task="t" :users="users"></task-item>
    </div>
</template>



<script>

import TaskItem from './TaskItem.vue'

export default {
    props:['tasks','users'],
    components:{
        TaskItem
    }
}
</script>

