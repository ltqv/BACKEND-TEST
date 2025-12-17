<script setup>


const props = defineProps({
  petCurent: {
    type: Object,
    required: true
  }
});

const emit = defineEmits(['save-pet', 'remove-pet']);

const savePet = () => {
  if (
    !props.petCurent.id ||
    !props.petCurent.name ||
    !props.petCurent.type ||
    props.petCurent.age === '' ||
    props.petCurent.weight === ''
  ) {
    alert('Vui lòng nhập đầy đủ thông tin thú cưng!');
    return;
  }
  emit('save-pet', { ...props.petCurent });
};

const removePet = () => {
  if (!props.petCurent.id) {
    alert('Chọn thú cưng cần xóa');
    return;
  }
  emit('remove-pet', props.petCurent.id);
};
</script>
<template>
  <div class="container">
    <form class="row g-3">
      <div class="col-md-6">
        <label for="inputId" class="form-label"><b>Mã thú cưng </b></label>
        <input type="text" class="form-control"  id="inputId" v-model="props.petCurent.id" placeholder="VD: PET03"
        />
      </div>

      <div class="col-md-6">
        <label for="inputName" class="form-label"><b>Tên thú cưng</b></label>
        <input type="text" class="form-control" id="inputName" v-model="props.petCurent.name" />
      </div>

      <div class="col-md-4">
        <label for="inputType" class="form-label"><b>Loài</b></label>
        <select  id="inputType"  class="form-select" v-model="props.petCurent.type"
        >
          <option value="Chó">Chó</option>
          <option value="Mèo">Mèo</option>
          <option value="Chuột Hamster">Chuột Hamster</option>
          <option value="Chim">Chim</option>
        </select>
      </div>

      <div class="col-md-4">
        <label for="inputAge" class="form-label"><b>Tuổi</b></label>
        <input type="number" class="form-control"  id="inputAge"  v-model.number="props.petCurent.age"  min="0"/>
      </div>

      <div class="col-md-4">
        <label for="inputWeight" class="form-label"><b>Cân nặng (kg)</b></label>
        <input type="number" class="form-control" id="inputWeight"  v-model.number="props.petCurent.weight" min="0" step="0.1" />
      </div>

      <div class="col-md-12">
        <label class="form-label me-3">Đã tiêm chủng</label>
        <div class="form-check form-check-inline">
          <input class="form-check-input" type="radio"  name="vaccinated" id="vaccinatedYes" :value="true"  v-model="props.petCurent.vaccinated"
          />
          <label class="form-check-label" for="vaccinatedYes">Đã tiêm</label>
        </div>
        <div class="form-check form-check-inline">
          <input class="form-check-input" type="radio" name="vaccinated" id="vaccinatedNo"  :value="false" v-model="props.petCurent.vaccinated"
          />
          <label class="form-check-label" for="vaccinatedNo">Chưa tiêm</label>
        </div>
      </div>

      <div class="col-12">
        <button type="button" class="btn btn-primary " @click="savePet">Save</button>
        <button type="button" class="btn btn-danger" @click="removePet" >  Delete</button>
      </div>
    </form>
  </div>
</template>
<style scoped>
</style>