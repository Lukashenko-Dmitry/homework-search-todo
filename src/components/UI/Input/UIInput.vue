<template>
      <div class="field">          
            <input
                v-model="value"
                @keyup.enter="emitValue"
                type="text"
                class="field-input"
                placeholder="Add task"
            />
            <font-awesome-icon 
                :icon="['fas','square-plus']"
                 @click="emitValue"
                :class="value.length > 3 ? 'add-task' : 'add-task__disabled'" 
            />
    </div>
</template>
<script>
export default {    
    data() {
        return {
            value: '',
            isActive:false,
            isDisabled:true,
        }
    },        
    methods: {
        emitValue() {
            if (this.value.length > 3){
                this.$emit('addTask', this.value);
                this.value = '';
            }            
        }
    }
}
</script>
<style lang="scss" scoped>
    @import 'UIInput.scss';
</style>
