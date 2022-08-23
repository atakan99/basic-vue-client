<template>
 <div>
  <input v-model="userForm.name" placeholder="name"/>
 </div>

  <div>
  <input v-model="userForm.age" placeholder="age"/>
 </div>

  <div>
  <button @click="onSubmit">Submit</button>
 </div>
</template>


<script >

export default {
    emits: ["onSubmit", "onUpdateAction"],
  data() {
    return {
      userForm: {
        name: undefined,
        age: undefined,
        id: undefined,
      },
    }
  },
 
  methods: {

    onSubmit() {
        console.log(this.userForm)
        this.$emit('onSubmit', this.userForm);
    },
    setUserData(userForm){
        this.userForm = {
            name: userForm.name,
            age: userForm.age,
            id: userForm._id
        }
        console.log(this.userForm)
    },
     clear() {
      this.userForm = {
        name: undefined,
        age: undefined,
        id: undefined,
      };
     }
  }
}

</script>

<style scoped>


</style>