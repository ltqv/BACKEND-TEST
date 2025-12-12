<script setup>
const props =defineProps({
    listUser:{
        type: Array,
        required: true
    }
});
const emit = defineEmits('selected-user')
const userSelected = (userId) =>{
    let userrow = props.listUser.find(e => e.id === userId);
    emit('selected-user',{...userrow});
    
}
</script>

<template>
<div class="container">
    <table class="table table-striped table-hover">
        <thead>
            <tr>
                <th>ID</th>
                <th>UserName</th>
                <th>Eamil</th>
                <th>Password</th>
                <th>Address</th>
                <th>Gender</th>
            </tr>
        </thead>
        <tbody>
            <tr v-for=" user in props.listUser" :key="user.id" @click="userSelected(user.id)">
                <td>{{ user.id }}</td>
                <td>{{ user.username }}</td>
                <td>{{ user.email }}</td>
                <td>{{ user.password }}</td>
                <td>{{ user.address }}</td>
                <td>{{ user.gender == 1 ? "Nu" : "Nam"}}</td>
                
            </tr>
        </tbody>
    </table>
</div>
</template>
<style scoped>

</style>
