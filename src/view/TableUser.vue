<script setup>

// props: Nhận mảng `listPet` từ app.vue truyền vào để hiển thị danh sách
const props = defineProps({
  listPet: {
    type: Array,
    required: true
  }
});
// emit: khai báo sự kiện 'selected-pet' để báo cho app.vue biết khi người dùng click vào một dòng
const emit = defineEmits('selected-pet');
// tìm object pet trong mảng listPet dựa trên id được click
// gửi event selected-pet kèm data của pet ra ngoài để app.vue update vào form input

const petSelected = (petId) => {
  const petRow = props.listPet.find((e) => e.id === petId);
  if (petRow) {
    emit('selected-pet', { ...petRow });
  }
};
</script>

<template>
  <div class="container">
    <table class="table table-striped table-hover">
      <thead>
        <tr>
          <th>Mã thú cưng</th>
          <th>Tên thú cưng</th>
          <th>Loài</th>
          <th>Tuổi</th>
          <th>Cân nặng (kg)</th>
          <th>Đã tiêm chủng</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="pet in props.listPet" :key="pet.id"  @click="petSelected(pet.id)">
          <td>{{ pet.id }}</td>
          <td>{{ pet.name }}</td>
          <td>{{ pet.type }}</td>
          <td>{{ pet.age }}</td>
          <td>{{ pet.weight }}</td>
          <td>{{ pet.vaccinated ? 'Đã tiêm' : 'Chưa tiêm' }}</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>
<style scoped>
</style>
