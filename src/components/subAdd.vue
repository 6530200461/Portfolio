<template>
  <h2 class="text-light bg-secondary text-center pt-2">เพิ่มวิชา</h2>
  <div>
    <div class="card">
      <div class="card-body">
        <form @submit.prevent="handleSubmit">
          <div class="row">
            <div class="col-lg-3 col-md-3 col-sm-4 mt-2">
              <label for="subId" class="form-label">รหัสวิชา:</label>
              <input type="text" class="form-control" id="subId" v-model.trim="subs.id">
            </div>
            <div class="col-lg-6 col-md-4 col-sm-6 mt-2">
              <label for="subName" class="form-label">ชื่อวิชา:</label>
              <input type="text" class="form-control" id="subName" v-model.trim="subs.name">
            </div>
            <div class="col-lg-2 col-md-3 col-sm-4 mt-2">
              <label for="subCradit" class="form-label">หน่วยกิต:</label>
              <select class="form-select" v-model="subs.cradit">
                <option disabled value="">เลือกหน่วยกิต</option>
                <option>1</option>
                <option>2</option>
                <option>3</option>
              </select>
            </div>
            <div class="col-lg-2 col-md-3 col-sm-4 mt-2">
              <label for="subGrade" class="form-label">เกรด:</label>
              <select class="form-select" v-model="subs.grade">
                <option disabled value="">เลือกเกรด</option>
                <option>A</option>
                <option>B+</option>
                <option>B</option>
                <option>C+</option>
                <option>C</option>
                <option>D+</option>
                <option>D</option>
                <option>F</option>
                <option>I</option>
              </select>
            </div>
            <div class="col-lg-3 col-md-3 col-sm-4 mt-2">
              <label for="subyr" class="form-label">ปีการศึกษา:</label>
              <input type="text" class="form-control" id="subyr" v-model.trim="subs.yr">
            </div>
            <div class="col-lg-2 col-md-3 col-sm-4 mt-2">
              <label for="subSem" class="form-label">ภาคเรียน:</label>
              <input type="text" class="form-control" id="subSem" v-model.trim="subs.sem">
            </div>
            <br>
            <button type="submit" class="btn btn-primary col-lg-1 col-md-3 col-sm-4 mt-5">บันทึก</button>
          </div>
        </form>
      </div>
    </div>

    <!-- Result message after adding subject -->
    <!-- <div class="row mt-3" v-if="showResultMessage"> -->
      <div v-if="addSuccess" class="alert alert-success br-primary" role="alert">
        <span class="font-weight-bold">บันทึกข้อมูลเรียบร้อยแล้ว</span>
      </div>

      <div v-if="addError" class="alert alert-danger" role="alert">
        เกิดข้อผิดพลาดในการบันทึกข้อมูล: {{ errorMessage }}
      </div>
    <!-- </div> -->
  </div>
</template>

<script>
export default {
  name: "subAdd",
  data() {
    return {
      subs: {
        id: "",
        name: "",
        cradit: "",
        grade: "",
        yr: "",
        sem: "",
        isShow: false,
      },
      addSuccess: false,
      addError: false,
      errorMessage: ""
    };
  },
  methods: {
    handleSubmit() {
      let Subject = {
        id: this.subs.id,
        name: this.subs.name,
        cradit: this.subs.cradit,
        grade: this.subs.grade,
        yr: this.subs.yr,
        sem: this.subs.sem,
        isShow: false
      };

      fetch('http://localhost:3000/Subject', {
        method: 'POST',
        headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify(Subject)
      })
        .then(() => {
          this.handleSuccessMessage();
        })
        .catch((err) => {
          this.addError = true;
          this.errorMessage = err;
        });
    },
    handleSuccessMessage() {
      this.addSuccess = true;
      setTimeout(() => {
        this.addSuccess = false;
      }, 3000);
    }
  }
};
</script>

<style></style>
