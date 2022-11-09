<template>
    <div id="todo-list">
        <div class="task">
            <div class="newtask">
                <h1>New Task</h1>
                <input type="text" v-model="newTask.name" class="todo-name" placeholder="Add New Task...">
                <label class="label-des">Description</label>
                <textarea v-model="newTask.des" class="todo-des"></textarea>
                <div class="date-pri">
                    <div class="due-date">
                        <label class="label-date">Due date</label>
                        <input type="date" v-model="newTask.date" class="todo-date">
                    </div>
                    <div class="priority">
                        <label class="label-priority">Priority</label>
                        <select name="Priority" id="Priority" v-model="newTask.pri" class="todo-priority">
                            <option value="Normal" selected>Normal</option>
                            <option value="Low">Low</option>
                            <option value="High">High</option>
                        </select>
                    </div>
                </div>
                <button @click="addTask()" class="btn">Add</button>
            </div>
        </div>
        <div class="todo">
            <div class="todo-task">
                <h1>To Do List</h1>
                <input type="text" v-model="search" placeholder="Search..." class="todo-search">
                <div v-for="(task,index) in filterTasks" :key="index" class="task-list">
                    <div class="task-name">
                        <input type="checkbox" v-model="task.done" class="check-list" @click="task.done = !isDone">
                        <input type="text" v-model="task.name" :disabled="inputDisabled" class="todo-name todo-item">
                        <button @click="isDetail = !isDetail" class=" edit-btn">Detail</button>
                        <button @click="removeTask(index)" class=" remove-btn">Remove</button>
                    </div>
                    <div class="task-detail" v-if="isDetail">
                        <input type="text" v-model="task.name" class="todo-name" :disabled="inputDisabled">
                        <label class="label-des">Description</label>
                        <textarea v-model="task.des" class="todo-des"></textarea>
                        <div class="date-pri">
                            <div class="due-date">
                                <label class="label-date">Due date</label>
                                <input type="date" v-model="task.date" class="todo-date">
                            </div>
                            <div class="priority">
                                <label class="label-priority">Priority</label>
                                <select name="Priority" id="Priority" v-model="task.pri" class="todo-priority">
                                    <option value="Normal">Normal</option>
                                    <option value="Low">Low</option>
                                    <option value="High">High</option>
                                </select>
                            </div>
                        </div>
                        <button @click="isDetail = !isDetail" class="btn">Update</button>
                    </div>

                    <div class="bulk-action" v-if="task.done==true">
                        <div class="bulk-action-detail">
                            <p>Bulk Action</p>
                            <button class="done-btn">Done</button>
                            <button @click="removeTask(index)" class=" remove-btn">Remove</button>
                        </div>
                    </div>
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
          search:'',
          tasks: [
              {name: 'toan la', des: 'hêheheh', date: '15/12/2022', pri: 'Normal', done: false},
              {name: 'olala', des: 'hêheheh', date: '15/12/2022', pri: 'Normal', done: false},
              {name: 'toan', des: 'hêheheh', date: '15/12/2022', pri: 'Normal', done: false},
          ],
          isDetail: false,
          isDone: false,
          inputDisabled: true,
      }
    },
    computed: {
        filterTasks: function() {
            return this.tasks.filter((task) => {
                return task.name.match(this.search);
            })
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
        box-sizing: border-box;
    }
    .task, .todo {
        display: inline-block;
        border: 1px solid #000;
    }

    .newtask {
        margin: 30px;
    }
    .todo-task {
        margin: 65px;
    }
    .newtask, .task-detail {
        display: flex;
        flex-direction: column;
        justify-content: center;
        width: 600px;
    }

    .task-list {
        display: block;
        box-sizing: border-box;
    }
    .task-name {
        display: flex;
        align-items: center;
    }
    .done {
        text-decoration: line-through;
    }
    h1 {
        font-size: 50px;
    }
    .todo-name {
        width: calc(100%-8px);
        height: 40px;
        font-size: 20px;
    }

    .label-des {
        text-align: left;
        font-weight: 700;
        margin: 30px 0 10px 0;
    }

    .todo-des {
        width: calc(100%-6px);
        height: 200px;
        border: 1px solid #000;
    }

    .date-pri {
        display: flex;
        justify-content: space-between;
    }

    .due-date, .priority {
        display: flex;
        flex-direction: column;
        width: 275px;
    }

    .label-date {
        text-align: left;
        font-weight: 700;
        margin: 30px 0 10px 0;
    }

    .todo-date {
        width: 100%;
        height: 38px;
        border: 1px solid #000;
    }

    .label-priority {
        text-align: left;
        font-weight: 700;
        margin: 30px 0 10px 0;
    }

    .todo-priority {
        width: 100%;
        height: 40px;
        border: 1px solid #000;
    }
    .btn {
        display: block;
        font-size: 30px;
        padding: 10px;
        margin-top: 50px;
        width: 100%;
        border-radius: 4px;
        border: none;
        color: #fff;
        background-color: #5cb85c;
    }

    .btn:hover {
        cursor: pointer;
    } 

    .todo-search {
        width: 646px;
        height: 40px;
        font-size: 20px;
    }
    .task-name {
        margin: 20px 20px 0 20px;
        border: 1px solid #000;
        width: 650px;
        height: 100px;
    }

    .task-detail {
        border: 1px solid #000;
        border-top: none;
        margin: 0 0 20px 20px;
        padding: 25px;
    }

    .bulk-action {
        position: absolute;
        top: auto;
        width: 600px;
        bottom: 30px;
        background-color: #BBB;
    }

    .bulk-action-detail {
        position: relative;
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