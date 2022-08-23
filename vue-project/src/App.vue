
<template>


 
 <!-- <div>
  <input v-model="userForm.name" placeholder="name"/>
 </div>

  <div>
  <input v-model="userForm.age" placeholder="age"/>
 </div>

  <div>
  <button @click="onSubmit">Submit</button>
  <button @click="onDelete">Delete</button>
 </div> -->

 <FormVue ref="refFormVue"  @onSubmit="onSubmit" />

 <br/>

 <TableVue :userFormList="userFormList" @onUpdate="onUpdate" @onDelete="onDelete"/>

</template>


<script >
// setup can be used for compositon api
// but now i will use options api
import axios from 'axios';
import TableVue from './components/Table.vue';
import FormVue from './components/Form.vue';
import Form from './components/Form.vue';

export default {
  name: 'App',
  components:{
    TableVue,
    FormVue,
    Form
},
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
    a() {

    },

    onGet() {
       axios.get('http://localhost:3000/api/userForm').then(
      (response) => {
        this.userFormList = response.data;
       
      }
    );
    },

    onSubmit(setUserForm) {
      console.log(setUserForm);
      let userFormToSend = {
        name: setUserForm.name,
        age: setUserForm.age,
      };
      if (setUserForm.id == null) {
         axios
      .post('http://localhost:3000/api/userForm', userFormToSend).then(
        (res) => 
        {
          console.log(res);
           window.location.reload();
            this.$refs.refFormVue.clear();

        }
      )
      } else {
        axios
      .put('http://localhost:3000/api/userForm/' + setUserForm.id, userFormToSend).then(
        (res) => 
        {
          console.log(res);
           window.location.reload();
           this.$refs.refFormVue.clear();
        }
      )
      }
   
    },
    onDelete(setUserForm) {
      console.log(setUserForm._id);
      axios.delete('http://localhost:3000/api/userForm/' + setUserForm._id).then(
        (res) => {
          console.log(res);
          window.location.reload();
        }
      )
    },
    onUpdate(userForm){
      this.$refs.refFormVue.setUserData(userForm);
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
