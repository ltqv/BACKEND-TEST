<script setup>
import { reactive } from 'vue';
import FormInput from './view/FormInput.vue';
import TableUser from './view/TableUser.vue';

// danh sách thú cưng ban đầu
const listPet = reactive([
  {
    id: 'PET01',
    name: 'Micky',
    type: 'Chó',
    age: 2,
    weight: 5.5,
    vaccinated: true
  },
  {
    id: 'PET02',
    name: 'Mimi',
    type: 'Mèo',
    age: 1,
    weight: 3.2,
    vaccinated: false
  }
]);

// thú cưng đang được nhập/sửa (binding 2 chiều với FormInput)
const petSelected = reactive({
  id: '',
  name: '',
  type: 'Chó',
  age: '',
  weight: '',
  vaccinated: true
});

const resetForm = () => {
  Object.assign(petSelected, {
    id: '',
    name: '',
    type: 'Chó',
    age: '',
    weight: '',
    vaccinated: true
  });
};

// save pet create or update
const handleSavePet = (newPet) => {
  const oldPet = listPet.find((e) => e.id === newPet.id);
  if (oldPet) {
    Object.assign(oldPet, newPet);
  } else {
    listPet.push({ ...newPet });
  }
  resetForm();
};

// event cờ lích dòng trên table
const handleSelectedPet = (petRow) => {
  Object.assign(petSelected, petRow);
};

// xóa thú cưng
const handleRemovePet = (petId) => {
  const idx = listPet.findIndex((e) => e.id === petId);
  if (idx !== -1) {
    listPet.splice(idx, 1);
  }
  resetForm();
};


</script>

<template>
  <FormInput
    :pet-curent="petSelected"
    @save-pet="handleSavePet"
    @remove-pet="handleRemovePet"
  />
  <hr />
  <br />
  <TableUser
    :list-pet="listPet"
    @selected-pet="handleSelectedPet"
  />
</template>

<style scoped></style>
