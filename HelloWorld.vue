<template>
<div class="container" style="max-width: 600px;">

<!-- headin start -->

<h2 class="text-center mt-5">My Vue ToDo App</h2>

<!-- input -->

<div class="d-flex" mt-5>
  <input 
  type="text" 
  v-model="task" 
  placeholder="Enter Task"
  class="w-100 form control">
  <button style="color: goldenrod;" @click="submitTask">SUBMIT</button>
</div>
<!-- task table -->
<table class="table table-bordered mt-5">
  <thead>
    <tr>
      <th scope="col">Task</th>
      <th scope="col" style="width: 120px;">Status</th>
      <th scope="col" class="text-center">Edit</th>
      <th scope="col" class="text-center">Delete</th>
    </tr>
  </thead>
  <tbody>
   
  
    <tr v-for="(task,index) in tasks" :key="index">
      
      
      <td>
        <span :class="{ 'line-through' :task.status==='finished'}">
        {{ task.name }}
        
        </span>
        
      </td>
      

      <td>
        <span
        class="pointer noselect"
        @click="changeStatus(index)"
        :class="{
          'text-danger' :task.status==='to-do',
          'text-success' :task.status==='finished',
          'text-warning' :task.status==='in-progress',
        }"
        >
           <!-- {{ capitalizeFirstChar(task.status) }} -->
        </span>
        
      </td>
      
      <td class="text-center">
        <div @click="editTask(index)">
          <!-- <span > Delete Icons</span> -->
          <button>Edit</button>
        </div>
      </td>

      <td class="text-center">
        <div @click="deleteTask(index)">
          <!-- <span >Edit Icons</span> -->
          <button>Delete</button>
        </div>
      </td>
    
      
      
    </tr>
    
  </tbody>
</table>
</div>
</template>

<script>
export default {
  name: 'HelloWorld',
  props:{
     msg:String,
  },
  data()
  {
    return {
      task:"",
      editedTask:null,
      statuses:["to-do","in-progress","finished"],
      
      tasks:[
        {
          name:"Hello Every One",
          status:"to-do",
        },
        {
          name:"Usman Muneer",
          status:"in-orogress",
        },
        {
          name:"Subscribr now",
          status:"finished",
        },
      ],
      
    };
  },
  methods:{
    capitalizeFirstChar(str){
      return str.charAt(0).toUppercase() + str.slice(1);
    },
    // change index
    changeStatus(index){
      let newIndex=this.statuses.indexOf(this.tasks[index].status);
      if(++newIndex > 2) newIndex=0;
      this.tasks[index].status=this.statuses[newIndex];
    },
    // delete tasks

    deleteTask(index){
      this.tasks.splice(index,1);
    },
    // eidt task

    editTask(index){
      this.task=this.tasks[index].name;
      this.editedTask=index;
    },
    submitTask() 
    {
      if(this.task.length === 0) return;
      if(this.editedTask !=null){
        this.tasks[this.editedTask].name=this.task;
        this.editedTask=null;
      } else{
     
          this.tasks.push({
            name:this.task,
            status:"todo",
          });
      }
      this.task="";
    },
  },

};




</script>


<style>

</style>
