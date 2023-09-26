<script>
  import Navbar from './components/layouts/Navbar.vue';
  import List from './components/components/List.vue';
  import Modal from './components/components/Modal.vue';
  import {ref} from "vue";
  export default {
    name: 'App',
    components: {
      Navbar,
      List,
      Modal
    },
    methods: {
      openConfirm (id) {
        console.log(id)
        this.currentTaskID = id;
        this.show = true;
      },
      
      closeConfirm()  {
        this.show = false 
      },
      getTask() {
        console.log(this.currentTaskID)
        let task = this.tasks.find(el=>el.id === this.currentTaskID);
        return task;
      },
      SaveFunc(task, priority, deadline, state) {
        console.log(task, priority, deadline);
        if(!task) return;
        const newTasks = [...this.tasks];
        console.log("!!!!!", state)
        newTasks.push({id:++this.i, task, priority, deadline, state});
        console.log("@@@@@@@@@", newTasks)

        this.tasks = newTasks
        console.log(this.tasks, )
      },

      updateTask(id, task, priority, deadline, state){
        this.tasks.forEach(el=>{
          if(el.id===id){
            el.task = task;
            el.priority = priority;
            el.deadline = deadline;
            el.state = state;
          }
        });
      },

      deleteTask(id){
        if(!id) return;
        this.tasks.forEach((el, i)=>{
          if(el.id == id){
            const newTasks = [...this.tasks];
            newTasks.splice(i, 1);
            this.tasks = newTasks;
          }
        }) 
      }
    },
    watch: {
      tasks(newValue, oldValue) {
        localStorage.setItem('tasks', JSON.stringify(newValue));
      }
    },
    data() {
      return {
        show: ref(false),
        currentTaskID: 0,
        HighPriorityFilter: false,
        MediumPriorityFilter: false,
        LowPriorityFilter: false,
        tasks: JSON.parse(localStorage.getItem('tasks')) ||  [
          {
            id: 1,
            task: "Running",
            priority: "High",
            deadline: "2023-09-27T21:57",
            state: "Ideation"
          },
          {
            id: 2,
            task: "Jumping",
            priority: "Medium",
            deadline: "12/10/23-13:00 PM",
            state: "Next Up"
          },
          {
            id: 3,
            task: "Dance",
            priority: "High",
            deadline: "12/10/23-13:00 PM",
            state: "In Progress"
          },
          {
            id: 4,
            task: "Cycling",
            priority: "Low",
            deadline: "12/10/23-13:00 PM",
            state: "Completed"
          },
          {
            id: 5,
            task: "Cycling",
            priority: "Low",
            deadline: "12/10/23-13:00 PM",
            state: "Ideation"
          },
        ],
        i: 5,
      }
    }
  };
</script>

<template>
  <Navbar brandName="Tacky" tagLine="A simple tool to track your tasks." tagLine2="(Inspired by Notion.io)" />
  <main>
    <h1>Total: {{ this.tasks.length }}</h1>
    <div class="filtering-div">
      <div>
        
        <input  v-model="HighPriorityFilter" type="checkbox" name="" id="High">  
        <label for="High">High</label>
      </div>
      <div>
        <input type="checkbox" v-model="MediumPriorityFilter" name="" id="Medium">  
        <label for="Medium">Medium</label>
      </div>
      <div>
        <input type="checkbox" v-model="LowPriorityFilter" name="" id="Low">  
        <label for="Low">Low {{ LowPriorityFilter }}</label>
      </div>
    </div>
    <Modal v-if="show" :closeFunc="closeConfirm" :deleteTask="deleteTask" :updateTask="updateTask" :saveFunc="SaveFunc" :task="getTask()"></Modal>
    <div class="lists">
      <List :tasks="tasks" :HighPriorityFilter="HighPriorityFilter" :MediumPriorityFilter="MediumPriorityFilter" :LowPriorityFilter="LowPriorityFilter" :show="show" :showTaskModal="openConfirm" :closeTaskModel="closeConfirm"  bgColor="#F0F0F0" type="Ideation" tagBgColor="#C6C6C6" />
      <List :tasks="tasks" :HighPriorityFilter="HighPriorityFilter" :MediumPriorityFilter="MediumPriorityFilter" :LowPriorityFilter="LowPriorityFilter" :show="show" :showTaskModal="openConfirm" :closeTaskModel="closeConfirm" bgColor="#FEE7D2" type="Next Up" tagBgColor="#FFBB7C" />
      <List :tasks="tasks" :HighPriorityFilter="HighPriorityFilter" :MediumPriorityFilter="MediumPriorityFilter" :LowPriorityFilter="LowPriorityFilter" :show="show" :showTaskModal="openConfirm" :closeTaskModel="closeConfirm" bgColor="#E8F1FF" type="In Progress" tagBgColor="#A6C9FF" />
      <List :tasks="tasks" :HighPriorityFilter="HighPriorityFilter" :MediumPriorityFilter="MediumPriorityFilter" :LowPriorityFilter="LowPriorityFilter" :show="show" :showTaskModal="openConfirm" :closeTaskModel="closeConfirm" bgColor="#E1FFE7" type="Completed" tagBgColor="#8FFFA8" />
    </div>
  </main>

</template>


<style>
  main{
    margin: 30px 20px;
  }
  .filtering-div{
    margin: 20px 0;
    display: flex;
    gap: 10px;
  }
  main .lists {
    /* background-color: aqua; */
    display: flex;
    flex-wrap: wrap;
    gap: 20px;
    justify-content: center;
  }
</style>


