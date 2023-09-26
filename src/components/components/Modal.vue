<template>
  <div class="modal">
    <div class="modal-content">
      <div class="modal-heading">
        <h2>Task Details</h2>
      </div>
      <div class="form-div">
        <div class="input-type">
          <div class="label">
            <label for="Task">Task</label>
          </div>
          <input type="text" v-model="taskName" placeholder="Enter Task Name" id="Task">
        </div>
        <div class="input-type">
          <div class="label">
            <label for="Priority">Priority</label>
          </div>
          <select v-model="taskPriority" placeholder="" id="">
            <option value=""></option>
            <option value="High">High</option>
            <option value="Medium">Medium</option>
            <option value="Low">Low</option>
          </select>
        </div>
        <div class="input-type">
          <div class="label">
            <label for="Priority">State</label>
          </div>
          <select v-model="state" placeholder="" id="">
            <option value=""></option>
            <option value="Ideation">Ideation</option>
            <option value="Next Up">Next up</option>
            <option value="In Progress">In Progress</option>
            <option value="Completed">Completed</option>
          </select>
        </div>
        <div class="input-type">
          <div class="label">
            <label for="deadline">Deadline</label>
          </div>
          <input type="datetime-local" v-model="taskDeadLine" id="deadline">
        </div>
        <div class="modal-buttons">
          <button class="modal-save-btn" @click="SaveFunc">Save</button>
          <button class="modal-delete-btn" @click="Delete">Delete</button>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
  export default {
        name: 'Modal',
        props: {
            closeFunc: Function,
            task: Object,
            saveFunc: Function,
            updateTask: Function,
            deleteTask: Function,
        },
        mounted() {
          this.pageLoadFunc()
        },
        methods: {
          Delete() {
            if(this.task){
              this.deleteTask(this.task.id);
              this.closeFunc();
            }
          },
          SaveFunc() {
            console.log(this.taskName, this.taskPriority, this.taskDeadLine, this.state)
            if(this.task){
              this.updateTask(this.task.id, this.taskName, this.taskPriority, this.taskDeadLine, this.state)
            }else{
              this.saveFunc(this.taskName, this.taskPriority, this.taskDeadLine, this.state);
            }
            this.closeFunc()
          },
          pageLoadFunc() {
            console.log(this.task, this.taskName)
          }
        },
        data() {
          return  {
            taskName: this.task?.task || "",
            taskPriority: this.task?.priority || "",
            taskDeadLine: this.task?.deadline || "",  
            state: this.task?.state || "",
          }
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
  .modal-heading h2{
    margin: 2px 0;
  }

  .modal-buttons {
    margin: 10px 0;
    display: flex;
    flex-direction: column;
    gap: 10px;
  }

  .modal-buttons .modal-save-btn, .modal-delete-btn {
    background-color: white;
    width: 300px;
    height: 30px;
    font-size: 16px;
    font-weight: 500;
    cursor: pointer;
    
  }

  .modal-buttons .modal-delete-btn:hover, .modal-save-btn:hover {
    outline: 2px solid black;
    border: none;
  }
  .modal-buttons .modal-delete-btn {
    color: red;
  }

  .form-div {
    margin: 20px 0;
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 10px;
    padding: 20px 0;
    padding-bottom: 0;
  }
.modal {
        position: absolute;
        top: 0;
        left: 0;
        background-color: rgba(0, 0, 0, 0.124);
        width: 100%;
        height: 100%;
        display: flex;
        justify-content: center;
        align-items: center;
        z-index: 99;
    }

    .modal-content {
        background-color: white;
        padding:10px 10px;
        padding-bottom: 0;
        width: 400px;
        height: fit-content;
        border-radius: 10px;
    }
    .input-type {
      display: flex;
    }

    .input-type .label {
      width: 70px;
      margin: 10px;
      font-size: 14px;
      font-weight: 500;
    }

    .input-type input, select {
      border: 1px solid gray;      
      width: 250px;
      height: 30px;
      padding: 0 5px;
    }

    .input-type select{
      width: 262px
    }

     option{
      margin: 100px 0;
    }

    .input-type input:focus, select:focus {
      outline: none;
    }
</style>
