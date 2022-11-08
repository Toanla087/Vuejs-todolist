<template>
    <div id="todo-list">
        <div class="task">
            <div class="newtask">
                <h1>New Task</h1>
                <input type="text" v-model="newTask.name" class="todo" placeholder="Add New Task...">
                <label>Description</label>
                <textarea v-model="newTask.des" ></textarea>
                <input type="date" v-model="newTask.date" >
                <select name="Priority" id="Priority" v-model="newTask.pri">
                    <option value="Normal" selected>Normal</option>
                    <option value="Low">Low</option>
                    <option value="High">High</option>
                </select>
                <button @click="addTask()" class="btn add-btn">Add</button>
            </div>
        </div>
        <div class="todo-task">
            <div v-for="(task,index) in tasks" :key="index" class="task-list">
                <div class="task-name">
                    <input type="checkbox" v-model="task.done" class="check-list">
                    <input type="text" v-model="task.name" :disabled="inputDisabled" :class="{done: task.done}" class="todo todo-item">
                    <button @click="inputDisabled = !inputDisabled" class="btn edit-btn">Edit</button>
                    <button @click="removeTask(index)" class="btn remove-btn">Remove</button>
                </div>
                <div class="task-detail">
                    <input type="text" v-model="task.name" class="todo" :disabled="inputDisabled">
                    <label>Description</label>
                    <textarea v-model="task.des" ></textarea>
                    <input type="date" v-model="task.date" >
                    <select name="Priority" id="Priority" v-model="task.pri" >
                        <option value="Normal">Normal</option>
                        <option value="Low">Low</option>
                        <option value="High">High</option>
                    </select>
                    <!-- <button @click="addTask()" class="btn add-btn">Add</button> -->
                </div>
            </div>
        </div>
    </div>
  </template>
  
  <script>
  export default {
    name: 'Todo',
    data() {
      return {
          newTask:{
            name:'',
            des:'',
            date: new Date().toISOString().slice(0,10),
            pri: 'Normal',
          },
          tasks: [
              {name: 'toan la', des: 'hêheheh', date: '15/12/2022', pri: 'Normal', done: false},
              {name: 'olala', des: 'hêheheh', date: '15/12/2022', pri: 'Normal', done: false},
              {name: 'toan', des: 'hêheheh', date: '15/12/2022', pri: 'Normal', done: false},
          ],
          inputDisabled: true,
      }
    },
    methods: {
        addTask: function() {
          this.tasks.push({
              name: this.newTask.name,
              des: this.newTask.des,
              date: this.newTask.date,
              pri: this.newTask.pri,
              done: false
          });
          this.newTask.name = '';
          this.newTask.des = '';
          this.newTask.date = new Date().toISOString().slice(0,10);
          this.newTask.pri = 'Normal';
        },
        removeTask: function(index) {
          this.tasks.splice(index, 1);
        },
    },
    props: {
      msg: String
    }
  }
  </script>
  
  <style scoped>
  #todo-list {
      background-color: #fafafa;
      display: flex;
      justify-content: center;
    }
    .task, .todo-task {
      display: inline-block;
    }
  .newtask {
    display: flex;
    flex-direction: column;
    justify-content: center;
    box-sizing: border-box;
  }

  .task-list {
    /* display: flex;
    flex-direction: ; */
    display: block;
    box-sizing: border-box;
  }
  .task-name {
    display: block;

  }
  .done {
      text-decoration: line-through;
  }
  h1 {
      font-size: 50px;
  }
  .todo {
      width: 52%;
      height: 40px;
      margin: 10px;
      font-size: 40px;
  }
  .btn {
      width: 10%;
      height: 100%;
      margin: 10px;
  }
  .btn:hover {
      cursor: pointer;
  } 
  .add-btn {
      font-size: 36px;
  }
  .check-list {
      width: 20px;
      height: 20px;
  }
  div .todo-item {
      font-size: 30px;
      border: none;
      width: 40%;
  }
  .edit-btn, .remove-btn {
      font-size: 30px;
  }
  </style>