<template>
<div class="wrapper">
<div class="header">
  <h1>app title</h1>
</div>
<div>
<table>
  <th>Name</th>
  <th>Email</th>
  <th>Edit</th>
  <th>Delete</th>
  <tbody>
    <tr v-for="row in tableRows"  v-bind:key="row">
      <td>
    <span v-show='!row.isEdit'>{{row.Name}}</span>
    <input v-show='row.isEdit' class="textInput" type="text" v-model="myInput.Name" @change="DisableEditing(row)"></td>
     <td>
    <span v-show='!row.isEdit'>{{row.Email}}</span>
    <input v-show='row.isEdit' class="textInput" type="text" v-model="myInput.Email" @change="DisableEditing(row)"></td>
    <td><img class="operations" src="./assets/Images/edit.jpg" v-on:click="EnableEditing(row.Name)"></td>
    <td><img class="operations" src="./assets/Images/delete.jpg" v-on:click="DeleteRow(row.Name)"></td>
    </tr>
  </tbody>
  </table>
</div>
<div>
  <button class="save" v-on:click="getUser()">Save</button>
  <button class="Cancel" v-on:click="getUser()">Cancel</button>
</div>
</div>
</template>
    
<script>
import Vue3EasyDataTable from "vue3-easy-data-table";
import "vue3-easy-data-table/dist/style.css";
export default {
  name: "App",
  components: {
    EasyDataTable: Vue3EasyDataTable,
  },
  
  data(){
    
  return{
  myInput : {Name:"",Email:""},
  tableRows: [
      { Name : 'Hema', Email:'abc@xyz.com', isEdit: false },
      { Name : 'Priya', Email:'abc@mno.com', isEdit: false} ]
}
  },
  methods:{
    EnableEditing(element){
      var currentRowIndex = this.tableRows.findIndex(x=>x.Name == element);
      this.tableRows[currentRowIndex].isEdit=true;
      this.myInput.Name = element;
      this.myInput.Email = this.tableRows[currentRowIndex].Email;

    },
    DisableEditing(element){
       var currentRowIndex = this.tableRows.findIndex(x=>x.Name == element.Name);
       this.tableRows[currentRowIndex].isEdit=false;
       this.tableRows[currentRowIndex].Name=this.myInput.Name;
       this.tableRows[currentRowIndex].Email=this.myInput.Email;
    },
    DeleteRow(element){
      var currentRowIndex = this.tableRows.findIndex(x=>x.Name == element);
      this.tableRows.splice(currentRowIndex,1);
    }
  }
};
</script>

<style>
.wrapper
{
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
}
.operations{
   width: 20px;
  cursor: pointer;
}
table{
  margin-left: 33%;
  margin-top: 3%;
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  height: 50%;
}
th{
  color: rgb(16, 56, 66);
}
td{
  width: 25%;
  text-align: center;
}
table, th, td {
  /* //border: 1px solid rgb(35, 142, 168); */
  border-collapse: collapse;
}

tr{
  height: 30%;
}

tr:nth-child(even) {
  background-color: rgba(150, 212, 212, 0.4);
}

th:nth-child(even),td:nth-child(even) {
  background-color: rgba(150, 212, 212, 0.4);
}
.header{
  height:80px;
  text-align: center;
  background-color: rgb(35, 142, 168);
}
.textInput{
  border-radius: 5px;
  border: 1px solid rgb(35, 142, 168);
  height: 100%;
}
.save{
     margin-left: 39%;
    margin-top: 2%;
    background-color: rgb(35, 142, 168);
    border-radius: 14px;
    height: 29px;
    width: 61px;
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    font-weight: bold;

}
.Cancel{
   margin-left: 1%;
    margin-top: 2%;
    background-color: rgb(35, 142, 168);
    border-radius: 14px;
    height: 29px;
    width: 61px;
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    font-weight: bold;
        

}
</style>
