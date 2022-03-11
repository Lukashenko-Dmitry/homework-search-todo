<template>
    <div 
        :is="isTag"
        class="task"
        >
       <div class="task-container">
            <component 
            class="task-container-check"
            :is="task.checked ? 'IconIsChecked' : 'IconIsNotChecked'"
            @click.native="$emit('changeIcon', { checked : task.checked, order })"
            />
            <p 
                :class="[task.checked && 'task-container-title__checked', 'task-container-title']"           
            >
                {{`${order}. id:${task.id} task:"${task.text}"`}}
            </p>
        </div>
        <div class="button-container">
            <button
                class="button-task"
                :disabled="task.checked" 
                @click="modalShow=true">
                Edit
            </button>
            <button
                class="button-task"
                :disabled="!task.checked"            
                @click="$emit('remove', order-1)">
                Remove
            </button>  
        </div>
        <Modal 
            v-if="modalShow"
            @close="closeModal"
            @saveTask="saveTask"            
            :task="task"
        />      
    </div>    
</template>

<script>
import IconIsChecked from '@/components/Task/UI/IconIsChecked/IconIsChecked'
import IconIsNotChecked from '@/components/Task/UI/IconIsNotChecked/IconIsNotChecked'
import Modal from "@/components/Task/UI/Modal/Modal.vue"

export default {
    components: {
      IconIsChecked,
      IconIsNotChecked,
      Modal,      
    },
    props:{
        task: {
            type: Object,
            required: true
        },
        order: {
            type:[String, Number],
            required: true,
        },
        isTag: {
            type: String,
            default: 'div',
        }
    },
    data (){
        return {
            modalShow:false,            
        } 
    },
    methods:{
        closeModal(){
            this.modalShow=false;
        },
        saveTask(taskTitle) {
            this.task.text = taskTitle                
            this.closeModal();
        }
    }
}
</script>

<style lang="scss" scoped>
@import 'Task.scss'
</style>

