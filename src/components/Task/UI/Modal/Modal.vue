<template>
    <div class="modal">
       <div class="modal-container">
        <h2 class="modal-title">Edit Task</h2>
        <p class="modal-text">Edit the title of this Task</p>
        <input 
            v-model="taskTitle" 
            class="modal-input" 
            type="text"
            @keyup.enter="$emit('saveTask', taskTitle)"
            >
        <button
            class="modal-button"
            @click="$emit('close')"
        >Cancel</button>
        <button
            class="modal-button"
            @click="$emit('saveTask', taskTitle)"
            :disabled="taskTitle === task.text || taskTitle.length < 3 || !taskTitle.trim()" 
            
        >Save</button>
       </div>
    </div>
</template>

<script>
export default {
    props:{
        task:{
            type: Object,
            required: true,
        }
    },
    data() {
        return {
            taskTitle: this.task.text
        }    
    },
    methods:{
       
    }
}
</script>

<style lang="scss" scoped>
    @import 'Modal.scss'
</style>