<template>
  <div class="container">
    <h2 class="text-centet mt-5">Todo App</h2>

    <div class="d-flex justify-content-center m-2">
      <span :class="{'fas fa-angle-double-down': task.displayMsg === 'EDIT Info'}">{{displayMsg}}</span>
    </div>

    <div class="d-flex">
      <input v-model="name" type="text" placeholder="Enter Task" class="form-control">
      <input v-model="tag" type="text" placeholder="Enter a Tag" class="form-control">
      <input v-model="desc" type="text" placeholder="Description" class="form-control">
      <button @click="newTask" class="btn-warning rounded-0">Submit</button>
    </div>

    <table class="table table-bordered mt-5">
      <thead>
        <tr>
          <th scope="col">Task</th>
          <th scope="col">Tag</th>
          <th scope="col">Decription</th>
          <th scope="col">Completed</th>
          <th scope="col" class="text-center">Edit</th>
          <th scope="col" class="text-center">Delete</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(task, index) in tasks" :key="index">
          <td>
            <span :class="{'finished': task.completed === true}">{{task.name}}</span>
            </td>
          <td>{{task.tag}}</td>
          <td>{{task.desc}}</td>
          <td>
            <div class="form-check">
              <input @click="completedTask(index)" v-model="completed" class="form-check-input pointer" type="checkbox" value="" id="flexCheckDefault">
              <label class="form-check-label" for="flexCheckDefault">
                It is done?
              </label>
            </div>
          </td>
          <td>
            <div class="text-center pointer" @click="editTask(index)">
              <span class="fa fa-pen"></span>
            </div>
          </td>
          <td>
            <div class="text-center pointer" @click="deteTask(index)">
              <span class="fa fa-trash"></span>
            </div>
          </td>
        </tr>
      </tbody>
    </table>

  </div>
</template>

<script>
export default {
  name: 'TodoApp',
  props: {
    msg: String
  },

  data(){
    return{
      task: '',
      editTaskIndex: null,
      displayMsg: '',
      tasks: [
        {
          name: "Do the thing!",
          tag: "Random",
          desc: "...the thing!!!",
          completed: false
        }
      ] 

    }
  },

  methods: {
    newTask(){
      if(this.name.length === 0) return;
      if(this.desc.length === 0) return;

      if(this.editTaskIndex == null){
        this.tasks.push({
          name: this.name,
          tag: this.tag,
          desc: this.desc,
          completed: false
        })
      } else{
        this.tasks[this.editTaskIndex].name = this.name
        this.tasks[this.editTaskIndex].tag = this.tag
        this.tasks[this.editTaskIndex].desc = this.desc
        this.editTaskIndex = null
        this.displayMsg = ''
      }
      
      this.name = ''
      this.tag = ''
      this.desc = ''

    },
    deteTask(index){
      this.tasks.splice(index, 1)
    },

    editTask(index){

      this.displayMsg = 'EDIT Info'
      
      this.name = this.tasks[index].name
      this.tag = this.tasks[index].tag
      this.desc = this.tasks[index].desc
      this.editTaskIndex = index
    },

    completedTask(index){
      let elm = document.getElementById('flexCheckDefault')
      console.log(elm.checked)
      if (elm.checked){
        this.tasks[index].completed = true
      } else{
        this.tasks[index].completed = false
      }
      
    }
  }


}
</script>

<style scoped>
.pointer{
  cursor: pointer;
}
.finished{
  text-decoration: line-through;
}
 
</style>
