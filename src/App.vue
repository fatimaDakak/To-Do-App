<template>
  <div class="container">
    <h2 class="text-center mt-5">My vue ToDo App</h2>
    <!--input-->
    <div class="d-flex">
      <input type="text" class="form-control m-2" placeholder="add your todo here" v-model="task">
      <button @click="AddTask" class="btn btn-secondary col-lg-2  m-2">Submit </button>
           

    </div>
    <!--todo-->
    <table class="table table-bordered mt-5 container">
  <thead>
    <tr>
      <th scope="col">Task</th>
      <th scope="col">Status</th>
      <th scope="col">Update</th>
      <th scope="col">Delete</th>
    </tr>
  </thead>
  <tbody v-for="(task, index) in tasks" :key="task">

    <tr>
      <th scope="row"><span :class="{'finished' : task.status=== 'finished'}">{{task.name}}</span></th>
      <td>
        <span  :class="{'text-danger' : task.status=== 'to-do','text-warning': task.status=== 'in-progress' }"
       class="pointer" @click="changeStatus(index)">
       {{firstCharUpper(task.status)}}
       </span>
       </td>
      <td><button @click=" setEditTask(index)"><i class="fas fa-pen-square"></i></button></td>
      <td><button @click="deleteTask(index)"><i class="far fa-trash-alt"></i></button></td>
    </tr>
    
   
  </tbody>
</table>

  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      task: '',
      tasks: [
        {
          name: "Practice Vue.js",
          status: 'to-do'
        },
        {
          name: "Have lunch with my mother",
          status: 'to-do'
        }
      ],
      available_stat: [
        'to-do',
        'in-progress',
        'finished'
      ],
      editTaskIndex: null,
    }
  },
  methods: {
    AddTask() {
      if (this.task.length === 0) return;

      if (this.editTaskIndex === null) {
        this.tasks.push({
          name: this.task,
          status: 'to-do'
        });
      } else {
        this.tasks[this.editTaskIndex].name = this.task;
        this.editTaskIndex = null;
      }

      this.task = ''; // Reset the input field after adding/updating the task
    },
    deleteTask(index) {
      this.tasks.splice(index, 1);
    },
    setEditTask(index) { // Renamed the method to setEditTask
      this.task = this.tasks[index].name;
      this.editTaskIndex = index;
    },
    changeStatus(index) {
      let newIndex = this.available_stat.indexOf(this.tasks[index].status);
      if (++newIndex > 2) newIndex = 0;
      this.tasks[index].status = this.available_stat[newIndex];
    },
    firstCharUpper(str) {
      return str.charAt(0).toUpperCase() + str.slice(1);
    }
  }
}
</script>


<style>
.pointer {
  cursor: pointer;
}
.finished{
  text-decoration: line-through;
}
</style>