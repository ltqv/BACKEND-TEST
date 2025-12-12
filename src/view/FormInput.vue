<script setup>

import { reactive } from 'vue';

const props = defineProps({
    userCurent:{
        type: Object,
        required: false,
        default: () => ({
                id: -1,
    username: '',
    email: '',
    password: '',
    address: '',
    gender: 0
        })
    }
})
const emit = defineEmits(['save-user' ,'remove-user']);




// chặn input không null
const saveUser = () => {
    if(!props.userCurent.id ||
        !props.userCurent.username ||
        !props.userCurent.email ||
        !props.userCurent.password ||
        !props.userCurent.address 
        
    ) {
        alert("vui long nhap data");
        return;
    }
    emit('save-user', {...props.userCurent});
    props.userCurent.id = 1;
    props.userCurent.username = '';
    props.userCurent.email = '';
    props.userCurent.password = '';
    props.userCurent.address = '';
    props.userCurent.gender = 0;

};

const removeUser = (userId) => {
    emit('remove-user', userId);
       props.userCurent.id = 1;
    props.userCurent.username = '';
    props.userCurent.email = '';
    props.userCurent.password = '';
    props.userCurent.address = '';
    props.userCurent.gender = 0;

}
</script>
<template>
<div class="container">
    <form class="row g-3">

          <div class="col-md-6">
            <label for="inputUserName" class="form-label"> UserName</label>
            <input type="text" class="form-control" id="inputUserName" v-model="props.userCurent.username">
        </div>

        <div class="col-md-6">
            <label for="inputEmail4" class="form-label"> Email</label>
            <input type="email" class="form-control" id="inputEmail4" v-model="props.userCurent.email">
        </div>

        <div class="col-md-4">
            <label for="inputPassword4" class="form-label">Password</label>
            <input type="password" class="form-control" id="inputPassword4" v-model="props.userCurent.password">
        </div>

        <div class="col-4">
            <label for="inputAddress" class="form-label">Address</label>
            <input type="text" class="form-control" id="inputAddress" v-model="props.userCurent.address">
        </div>

        <div class="col-md-4">
            <label for="inputGender" class="form-label" >Gender</label>
            <select id="inputState" class="form-select" v-model="props.userCurent.gender">
                <option selected value="0">Male</option>
                <option value="1">Female</option>
            </select>
        </div>

        
        <div class="col-12">
            <button type="button" class="btn btn-primary" @click="saveUser">Save</button>
            <button type="button" class="btn btn-danger" @click="removeUser">Remove</button>
        </div>
    </form>
</div>
</template>
<style  scoped>
    
</style>