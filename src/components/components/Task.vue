<template>
    <div class="task" :style="{backgroundColor: show ? '#E7E7E7' : '#FFFFFF'}">
        <h4>{{ task }}</h4>
        <hr>
        <div class="task-details">
            <h5 :style="{color: textColor}">{{ priority }}</h5>
            <p>{{ deadline }}</p>
        </div>
    </div>

</template>

<script>
    export default {
        name: 'Task',
        props: {
            task: String,
            priority: String,
            deadline: String, 
            show: Boolean,
        },
        computed: {
            textColor() {
                if (this.priority === 'High') {
                    return '#FF5151';
                } else if(this.priority === "Medium"){
                    return '#FF7425';
                }else{
                    return '#1DD300'
                }
            }
        },
        
    };
</script>

<style>
    h4, h5 {
        margin: 0;
    }
    .task {
        width: 280px;
        padding: 10px;
        border-radius: 15px;
        cursor: pointer;
        position: relative;
    }


    .task h1 {
        margin: 0;
    }
    .task .task-details {
        display: flex;
        justify-content: space-between;
        align-items: center;
    }

    .task .task-details p{
        font-size: 12px;
        font-weight: 500;
    }
</style>