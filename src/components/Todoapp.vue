<template>
  <div class="container">
    <h2 class="text-center-mt-S">My Vue Todo App</h2>

    <!-- Input -->
    <div class="d-flex">
      <input v-model="task" type="text" class="form-control" placeholder="enter task">
      <button @click="submitTask" class="btn btn-warning rounded-0">Submit</button>
    </div>

    <!-- Task Table -->
    <table class="table table-bordered">
  <thead>
    <tr>
      <th scope="col">Task</th>
      <th scope="col">Status</th>
      <th scope="col" class="text-center">#</th>
      <th scope="col" class="text-center">#</th>
    </tr>
  </thead>
  <tbody>
    <tr v-for="(task, index) in tasks" :key="index">
      <th>{{ task.name }}</th>
      <td style="width = 120px"><span class="pointer" @click="changeStatus(index)">{{ task.status }}</span></td>
      <td>
        <div class="text-center" @click="editTask(index)">
          <span class="fa fa-pen"></span>
        </div>
      </td>
      <td>
        <div class="text-center" @click="deleteTask(index)">
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
  name: 'HelloWorld',
  props: {
    msg: String
  },

  data(){
    return {
        task: "",
        editedTask: null,
        availableStatuses : ['to-do','in-progress', 'finished'],

        tasks: [
          {
          name: "Makan pagi",
          status: "to-do",
         },
         {
          name: "Makan Malam",
          status: "in-progress",
         }
        ]}
    
  },

  methods: {
    submitTask(){
      if(this.task.lenght === 0) return;

      if(this.editedTask === null){
      this.tasks.push({
        name: this.task,
        status: 'to-do'
      });
      }else{
        this.tasks[this.editedTask].name = this.task;
        this.editedTask = null;
      }

      this.task = '';
    },

    deleteTask(index){
      this.tasks.splice(index, 1);
    }

  },

    editTask(index){
      this.task = this.tasks[index].name;
      this.editedTask = index;
    },
    changeStatus(index){
     let newIndex = this.availableStatuses.indexOf(this.tasks[index].status);
     if(++newIndex > 2) newIndex = 0;
     this.tasks[index].status = this.availableStatuses[newIndex];
    }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.pointer{
  cursor: pointer;
}
</style>
