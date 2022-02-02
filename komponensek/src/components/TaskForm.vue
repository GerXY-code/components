<template>
    <form @submit.prevent="save">
        <input type="text" v-model="task.title" :class="{invalid:errors.titleErr}">
        <p v-if="errors.titleErr" class="errormsg">{{errors.titleErr}}</p>
        <br>
        <select v-if="!loading" v-model="task.assigneeId" :class="{invalid:errors.assigneIdErr}">
            
            <option v-for="u in users" :key="u.id" :value="u.id">{{u.name}}</option>
           
            
        </select>
         
        <span v-else>Az elemek töltés alatt! Kérlek várj...</span>
        <p v-if="errors.assigneIdErr" class="errormsg">{{errors.assigneIdErr}}</p>
        <br>
        <textarea v-model="task.description" :class="{invalid:errors.descErr}"></textarea>
        <p v-if="errors.descErr" class="errormsg">{{errors.descErr}}</p>
        <br>
        <button type="submit">Adatok beküldése</button>
    </form>

</template>


<script>
export default {
    props:['maxId','users','loading'],
    data(){
        return{
                task:{
                    title:'',
                    assigneeId:null,
                    description:''
            },
            errors:{
                titleErr:'',
                assigneIdErr:'',
                descErr:''
            }
        }
            
    },
    methods:{
        validate(){
            this.errors.titleErr=null
            this.errors.assigneIdErr=null
            this.errors.descErr=null

            if(!this.task.title){
                this.errors.titleErr="Nem lehet üres ez a mező!"
            }
            else if(this.task.title.length>=100){
                this.errors.titleErr="Maximum 99 karakteres lehet ez a mező!"
            }

            if(this.task.assigneeId == null){
                this.errors.assigneIdErr="Kötelezően választanod kell egyet!"
            }
             if(!this.task.description){
                this.errors.descErr="Nem lehet üres ez a mező!"
            }
            else if(this.task.description.length<=10){
                this.errors.descErr="Minimum 11 karakteres kell legyen a leírás!"
            }
            

            return this.errors.titleErr == null && this.errors.assigneIdErr == null  && this.errors.descErr==null

    },
         save(){
            if(!this.validate()){
                return
            }

            const taskObj = {
                id:this.maxId,
                title:this.task.title,
                assigneId:this.task.assigneeId,
                desc:this.task.description,
                closed:false

            }
                
            this.$emit('save',taskObj)

            this.task.title='',
            this.task.assigneeId=null,
            this.task.description=''
    }   
    }
    
}
</script>

<style>

.invalid{
    border:3px solid red;
    color:red;   
}
.errormsg{
    color:red;
}
</style>



