
<template>
 
 <div>
  <input v-model="userForm.name" placeholder="name"/>
 </div>

  <div>
  <input v-model="userForm.age" placeholder="age"/>
 </div>

  <div>
  <button @click="onGet">Get</button>
  <button @click="onSubmit">Submit</button>
  <button @click="onDelete">Delete</button>
 </div>


</template>


<script >
// setup can be used for compositon api
// but now i will use options api
import axios from 'axios';

export default {
  name: 'App',
  mounted(){
   this.onGet();
  },
  data() {
    return {
      userForm: {
        name: '',
        age: '',
      },
      id: '',
      userFormList: [],
    }
  },
  methods: {

    onGet() {
       axios.get('http://localhost:3000/api/userForm').then(
      (response) => {
        this.userFormList = response.data;
        if (this.userFormList.length > 0) {
          this.userForm.age = this.userFormList[0].age;
          this.userForm.name =  this.userFormList[0].name;
          this.id = this.userFormList[0]._id;
          console.log(this.id);
        }else{
          alert('db is empty');
        }
       
      }
    );
    },

    onSubmit() {
      if (this.id === '') {
            axios
      .post('http://localhost:3000/api/userForm', this.userForm).then(
        (res) => 
        {
          console.log(res);
        }
      )
      } else {
        axios
        .put('http://localhost:3000/api/userForm/' + this.id, this.userForm).then(
          (res) => 
          {
            console.log(res);
          }
        )
      }
      window.location.reload();
    
   
    },
    onDelete (){
      if(this.id === ''){
        alert('Nothing to delete');
        return;
      }
      axios
      .delete('http://localhost:3000/api/userForm/' + this.id).then(
        (res) => 
        {
          console.log(res);
        }
      )
      this.clear()
      window.location.reload();
        
    },
     clear() {
      this.id='';
      this.userFormList = [];
      this.userForm = {
        name: '',
        age: '',
      };
     }
  }
}



</script>

<style scoped>


</style>
