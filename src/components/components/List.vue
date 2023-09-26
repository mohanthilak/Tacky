<template>
    <div class="list" :style="{ backgroundColor: bgColor }" @drop="onDrop($event, type)" @dragenter.prevent @dragover.prevent>
        <div class="list-tag" :style="{ backgroundColor: tagBgColor }">
            <img src="../../assets/dot.svg" width="5" height="5" alt="Dot SVG">
            <p>{{ type }}</p>
        </div>
        <div class="tasks" >
            
            <Task  v-for="task in getMatchingTasks()" @click="showTaskModal(task.id)" :show="show"  :key="task.id" :task="task.task" :priority="task.priority" :deadline="task.deadline" draggable="true" @dragstart="startDrag($event, task)" />
        </div>
        <div class="add-task-div">
            <Icon @click="showTaskModal()" class="icon-icon" icon="la:plus" width="32" color="#373738" />
        </div>
    </div>
</template>

<script>
import Task from './Task.vue';
import { Icon } from '@iconify/vue';
    export default {
    name: 'List',
    props: {
        type: String,
        bgColor: String,
        tagBgColor: String,
        tasks: Array,
        showTaskModal: Function,
        closeTaskModel: Function,
        show: Boolean,
        LowPriorityFilter: Boolean,
        MediumPriorityFilter: Boolean,
        HighPriorityFilter: Boolean,
    },
    components: { Task, Icon },
    methods: {
        getMatchingTasks() {
            return this.tasks.filter(task => {
                if(task.state === this.type){
                    if(!this.LowPriorityFilter && !this.MediumPriorityFilter && !this.HighPriorityFilter) return true;
                    if(this.LowPriorityFilter && task.priority == "Low") return true; 
                    if(this.HighPriorityFilter && task.priority == "High") return true; 
                    if(this.MediumPriorityFilter && task.priority == "Medium") return true; 
                };
            })
        },
        onDrop (event, state) {
            const id = event.dataTransfer.getData('id')
            this.tasks.forEach(el => {
                if(el.id == id)el.state = state
            });
            
        },
        startDrag (event, item){
        event.dataTransfer.dropEffect = "move"
        event.dataTransfer.effectAllowed = "move"
        event.dataTransfer.setData('id', item.id)
        }
    },
    
};
</script>
<style>
    .list{
        height: fit-content;
        width: 300px;
        min-height: 100px;
        padding: 15px;
        border-radius: 15px;
    }

    .list .list-tag {
        display: flex;
        align-items: center;
        width: fit-content;
        padding: 3px 20px 3px 10px;
        border-radius: 15px;
    }

    .list .list-tag p {
        font-weight: 600;
        font-size: 16px;
    }
    .list .list-tag img {
        margin-right: 5px;
    }
    .add-task-div {
        display: flex;
        justify-content: center;
        margin-top: 10px;
    }
    
    .add-task-div .icon-icon {
        cursor: pointer;
    }
    
    .task {
        margin: 20px 0;
    }
</style>