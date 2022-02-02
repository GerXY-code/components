<template>
    <div>
       
        <label :class="{closed:task.closed}">

        
        <span>Feladat címe: </span>{{task.title}}
        <br>
        <span>Feladat leírása: </span>{{task.desc}}
        <br>
        {{ getUserById(task.assigneId) }}
        <span>Feladathoz rendelt név: </span>{{user.name}}
    
            
        <br>
        <span>Feladat lezárása: </span> <input type="checkbox" v-model="task.closed">
        <br>
        
         </label>
    </div>
</template>

<script>
export default {
    props:['task','users'],
    data(){
        return{
            user:""
        }
    },
    methods:{
        getUserById(id) {
            
           this.user  = this.users.find(l => l.id === id)
            


        },
    }
}
</script>


<style scoped>
    .closed{
        opacity:0.3;
    }
    span{
        font-weight: bold;
    }
</style>