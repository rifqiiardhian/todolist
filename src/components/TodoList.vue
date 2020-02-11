<template>
  <div class="container">
    <div class = "header">
      <h1>TO DO LIST </h1>
      <p class = "desc">DO WHAT YOU LOVE AND SO MANY REASONS TO BE HAPPY</p>
    </div>
    <div class="tambah-data">
      <div class="form-tambah">
        <h2>Enter Your Task Here</h2>
        <form @submit.prevent="addData">
          <input type="text" placeholder="Task Title" v-model="taskData"/>
          <br/>
          <input type="text" placeholder="Courses" v-model="coursesData"/>
          <br/>
          <input type="text" placeholder="Description" v-model="descriptionData"/>
          <br />
          <p>Due Date</p>
          <input type="date" placeholder="Deadline" v-model="deadlineData"/>
          <br/>
          <button class="btn-add" @click="addData">ADD</button>
        </form>
      </div>
      <p>(C) 2020 Created by Rifqi Ardhian</p>
    </div>
    <div class="todo-list">
      <div class="item" v-for="(item, index) in todoList" :key="index">
        <div class="card-todo">
          <div class="col-8">
          <h2 style="text-align: left">{{item.task}}</h2>
          <p style="text-align: left">{{item.courses}} | Due Date : {{item.deadline}}</p>
          <p style="text-align: left">{{item.description}}</p>
          </div>
          <div class="col-4">
            <button class="btn-remove" @click="removeData(item)" >DELETE</button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>export default {
  data: () => ({
    taskData: '',
    coursesData: '',
    deadlineData: '',
    descriptionData: '',
    todoList: [],
  }),
  created() {
    this.loadlocalStorage();
  },
  watch: {
    todoList() {
      localStorage.setItem('todoList', JSON.stringify(this.todoList));
    },
  },
  methods: {
    addData() {
      if (this.taskData !== '') {
        const date = new Date();
        const dataTask = {
          id: date.getTime(),
          task: this.taskData,
          courses: this.coursesData,
          deadline: this.deadlineData,
          description: this.descriptionData,
          complete: false,
          show: false,
        };
        this.todoList.push(dataTask);
      }
      this.taskData = '';
      this.coursesData = '';
      this.deadlineData = '';
      this.descriptionData = '';
    },
    removeData(item) {
      const index = this.todoList.findIndex((Element) => Element.id === item.id);
      this.todoList.splice(index, 1);
    },
    loadlocalStorage() {
      const ls = JSON.parse(localStorage.getItem('todoList'));
      if (ls == null) {
        return;
      }
      this.todoList = ls;
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.container {
  margin: 10px;
  display: grid;
  grid-template-columns: repeat(2, 1fr);
}
.header {
  grid-column: 1/3;
  border: 2px solid #4a8ba1;
  padding: 20px;
  margin-bottom: 10px;
  background-color: #4a8ba1;
}
.tambah-data {
  width: 550px;
  text-align: center
}
.form-tambah {
  box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2);
  padding-top: 10px;
}
.todo-list {
  width: 750px;
}
input[type=text],input[type=date] {
  height: 30px;
  margin: 5px;
  padding: 5px;
  cursor: pointer;
  transition: 0.3s;
  width: 450px;
}
input[type=text]:focus {
  border: 2px solid dodgerblue;
  border-radius: 0px;
}
.btn-add{
    background-color: transparent;
    color: grey;
    border: 2px solid grey;
    border-radius: 0px;
    text-align: center;
    margin: 5px 2px;
    padding: 10px 15px;
    cursor: pointer;
    transition: 0.3s;
    margin: 20px;
    width: 300px;
}
.btn-add:hover{
    background-color: #42d100;
    border: 2px solid #42d100;
    color: white;
}
.card-todo {
    box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2);
    transition: 0.3s;
    display: grid;
    grid-template-columns: repeat(2, 1fr);
    grid-auto-rows: minmax(10px, auto);
    margin-bottom: 20px;
    background-color: #f5f5f5;
}
.col-8 {
  padding-left: 10px;
  width: 600px;
}
.card-todo:hover {
    box-shadow: 0 8px 16px 0 rgba(0,0,0,0.2);
}
.btn-remove{
    background-color: transparent;
    color:grey;
    border: 2px solid grey;
    border-radius: 0px;
    text-align: center;
    margin: 5px 2px;
    padding: 10px 15px;
    cursor: pointer;
    transition: 0.3s;
    margin: 20px;
}
.btn-remove:hover{
    background-color: red;
    border: 2px solid red;
    color: white;
}
h1 {
  color: white;
}
h2 {
  color: #00074a;
}
.desc {
  color: white;
}
</style>
