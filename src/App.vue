<script setup>
  import { reactive } from 'vue';
import FormInput from './view/FormInput.vue';
import TableUser from './view/TableUser.vue';

  const listUser = reactive([
    {
      id: 1, username: 'ltqv',
      email: 'ltqv@gmail.com', 
      password: '1234',
      address: 'HCMCT', 
      gender: 0
    }

  ]);

  const userSelected = reactive({
    id: -1,
    username: '',
    email: '',
    password:'',
    address: '',
    gender: 0,
  });
  const handleSaveUser = (newUser) => {
    //update
    let olduser = listUser.find(e => e.id === newUser.id);
    if(olduser){
      Object.assign(olduser, newUser);
    } else {
   //create
newUser.id = Math.floor(Math.random()*100) + 1; //random id 1-100
listUser.push(newUser);
    }
 
  };

  const handleSelectedUser = (userRow) => {
Object.assign(userSelected, userRow);
  };

  const handleRemoveUser = (userId) => {
    let userInList = listUser.findIndex(e => e.id == userId)
    if(userInList){
      listUser.splice(userInList, 1);
    }

  };
  
</script>

<template>
<FormInput 
:user-curent="userSelected" 

@save-user="handleSaveUser"
@remove-user="handleRemoveUser"
/>
<hr>
<br>
<TableUser :list-user="listUser" 
@selected-user="handleSelectedUser"
/>           
</template>

<style scoped></style>
