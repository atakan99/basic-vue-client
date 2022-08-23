
<template>

 <FormVue ref="refFormVue"  @onSubmit="onSubmit" />

 <br/>

 <TableVue :userFormList="userFormList" @onUpdate="onUpdate" @onDelete="onDelete"/>

</template>


<script >
// setup can be used for compositon api
// but now i will use options api
import axios from 'axios';
import TableVue from './Table.vue';
import FormVue from './Form.vue';

export default {
  name: 'App',
  components:{
    TableVue,
    FormVue,
},
  mounted(){
   this.onGet();
  },
  data() {
    return {
      userFormList: [],
    }
  },
  methods: {
  
    onGet() {
       axios.get('http://localhost:3000/api/userForm').then(
      (response) => {
        this.userFormList = this.parseResponseData(response.data);   
      }
    );
    },

    parseResponseData(data){
        if(data.length === 0){
            return data;
        }
        return data.map( (item) => {
            return {
                name: item.name,
                age: item.age,
                id: item._id
            }
        } );
    },  

    onSubmit(setUserForm) {
      let userFormToSend = {
        name: setUserForm.name,
        age: setUserForm.age,
      };
        if (setUserForm.id == null) {
            axios
        .post('http://localhost:3000/api/userForm', userFormToSend).then(
            (res) => 
            {
                window.location.reload();
                this.$refs.refFormVue.clear();
            })
        } else {
            axios
        .put('http://localhost:3000/api/userForm/' + setUserForm.id, userFormToSend).then(
            (res) => 
            {
            window.location.reload();
            this.$refs.refFormVue.clear();
            })}
    },

    onDelete(setUserForm) {
      axios.delete('http://localhost:3000/api/userForm/' + setUserForm.id).then(
        (res) => {
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
     }
  }
}



</script>

<style scoped>


</style>
