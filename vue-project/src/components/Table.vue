<template>
<div>
 <table>
  <tr>
    <th>Name</th>
    <th>Age</th>
    <th>Update Operation</th>
    <th>Delete Operation</th>
  </tr>
  <tr v-for="userForm in userFormList">
    <td> {{userForm.name}} </td>
    <td> {{userForm.age}} </td>
    <td> <button @click="onUpdate(userForm)"> Update </button> </td>
    <td> <button @click="onDelete(userForm)"> Delete </button> </td>
  </tr>
</table>
</div>

</template>


<script >

export default {
    props:{
        userFormList: {
            type: Array,
            required: true
        }
    },
    methods:{
        onUpdate(userForm){
            this.$emit('onUpdate', userForm);
        },
        onDelete(userForm){
            this.$emit('onDelete', userForm);
        }
    }
}

</script>

<style scoped>
table {
  font-family: arial, sans-serif;
  border-collapse: collapse;
  width: 50%;
  padding-bottom: 10px;
}

td, th {
  border: 1px solid #dddddd;
  text-align: left;
  padding: 8px;
}

tr:nth-child(even) {
  background-color: #dddddd;
}

</style>
