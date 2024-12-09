<template>
  <div class="card my-2">
    <div class="card-body bg-secondary bg-opacity-10">
      <h5 class="card-title">รหัสวิชา {{ Subject.id }}</h5>
      <div class="form-group row">
        <label for="name" class="col-sm-2 col-form-label">ชื่อวิชา:</label>
        <div class="col-sm-10">
          <input v-if="editing" type="text" class="form-control" id="name" v-model.trim="Subject.name">
          <span v-else class="form-control-plaintext">{{ Subject.name }}</span>
        </div>
      </div>
      <div class="form-group row">
        <label for="cradit" class="col-sm-2 col-form-label">หน่วยกิต:</label>
        <div class="col-sm-10">
          <input v-if="editing" type="number" class="form-control" id="cradit" v-model.trim="Subject.cradit">
          <span v-else class="form-control-plaintext">{{ Subject.cradit }}</span>
        </div>
      </div>
      <div class="form-group row">
        <label for="grade" class="col-sm-2 col-form-label">เกรด:</label>
        <div class="col-sm-10">
          <input v-if="editing" type="text" class="form-control" id="grade" v-model.trim="Subject.grade">
          <span v-else class="form-control-plaintext">{{ Subject.grade }}</span>
        </div>
      </div>
      <div class="form-group row">
        <label for="yr" class="col-sm-2 col-form-label">ชั้นปี:</label>
        <div class="col-sm-10">
          <input v-if="editing" type="number" class="form-control" id="yr" v-model.trim="Subject.yr">
          <span v-else class="form-control-plaintext">{{ Subject.yr }}</span>
        </div>
      </div>
      <div class="form-group row">
        <label for="sem" class="col-sm-2 col-form-label">เทอม:</label>
        <div class="col-sm-10">
          <input v-if="editing" type="number" class="form-control" id="sem" v-model.trim="Subject.sem">
          <span v-else class="form-control-plaintext">{{ Subject.sem }}</span>
        </div>
      </div>
    </div>
    <button v-if="!editing" class="btn btn-warning mt-3 col-lg-1 col-md-3 col-sm-6" @click="editDetail()">
      แก้ไขข้อมูล
    </button>
    <button v-else class="btn btn-success mt-3 col-lg-1 col-md-3 col-sm-6" @click="saveEdit()">
      บันทึก
    </button>
    <button class="btn btn-danger mt-3 col-lg-1 col-md-3 col-sm-6" @click.prevent="delDetail()">
      ลบข้อมูล
    </button>
    <div v-if="delSuccess" class="alert alert-success br-primary" role="alert">
      <span class="font-weight-bold">ลบข้อมูลเรียบร้อยแล้ว</span>
    </div>
  </div>
</template>

<script>
export default {
  name: 'subDetail',
  props: ['subId'],
  data() {
    return {
      Subject: {},
      editing: false,
      delSuccess: false
    }
  },
  mounted() {
    this.fetchSubject(this.subId);
  },
  methods: {
    fetchSubject(subId) {
      fetch('http://localhost:3000/Subject/' + subId)
        .then(res => res.json())
        .then(data => this.Subject = data)
        .catch(err => console.log(err.message))
    },
    editDetail() {
      this.editing = true;
    },
    saveEdit() {
      this.editing = false;
      fetch('http://localhost:3000/Subject/' + this.subId, {
        method: 'PUT',
        headers: {
          'Content-Type': 'application/json'
        },
        body: JSON.stringify(this.Subject)
      })
        .then(() => {
          this.$emit('editing');
        })
        .catch(err => console.log(err.message));
    },
    delDetail() {
      fetch('http://localhost:3000/Subject/' + this.subId, {
        method: 'DELETE'
      })
        .then(() => {
          this.delSuccess = true;
          setTimeout(() => {
            this.delSuccess = false;
          }, 3000);
          this.$emit('delete');
        })
        .catch(err => console.log(err.message));
    },
  }
}
</script>

<style>
.card {
  border: 1px solid #ccc;
  border-radius: 4px;
  padding: 10px;
}

.card-body {
  padding: 15px;
}

.card-title {
  font-weight: bold;
  margin-bottom: 15px;
}

.form-group {
  margin-bottom: 15px;
}

.btn {
  margin-right: 10px;
}
</style>
