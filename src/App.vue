<template>
  <div id="app">
    <div class="container">
      <div class="app">
        <div class="app-header">        
            <h1 class="app-header__title">List of tasks</h1>            
            <UIInput 
              @addTask="addTask"
            />
            <input 
              v-show="tasks.length"
              class="app-header__search" 
              type="text" 
              v-model="search" 
              placeholder="Search the task"
            >   
        </div>
      <div class="app-tasklist">  
        <ul class="app-tasklist__list" v-if="!!tasks.length" >  
          <Task
            v-for="(item, index) of filterTasks"
            :key="item.id"
            :task="item"
            :order="index+1"
            is-tag="li"
            @changeIcon="changeIcon"
            @remove="removeTask"
          />
        </ul>
      </div>
      </div>
    </div>    
  </div>  
</template>
<script>

import UIInput from "@/components/UI/Input/UIInput.vue";
import Task from "@/components/Task/Task.vue";

export default {
  components: { 
    UIInput,
    Task,   
  },
  data() {
    return{
      tasks:[],
      search:''     
    }   
  },
  methods:{
    addTask(text) {
      this.tasks.push({
        id: Math.floor(Math.random() * 1000),
        text,
        checked: false,
      })
    },
    changeIcon({checked, order}) {
      this.tasks[order-1].checked = !checked;
    },
    removeTask(index) {
      this.tasks.splice(index, 1);
    }
  },
  computed:{
    filterTasks() {
        return this.tasks.filter(task => task.text.toLowerCase().indexOf(this.search.toLowerCase()) != -1)
      }
    },
};
</script>
<style lang="scss">
  @import "App.scss";
</style>

