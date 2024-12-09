<template>
  <div class="bar">
    <section id="navbar">
      <nav class="navbar navbar-expand-lg bg-info-subtle" id="navbar">
        <div class="container">
          <a class="navbar-brand" href="#"><i class="bi bi-alexa"></i>Portfolio Home</a>
          <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarNav"
            aria-controls="navbarNav">
            <span class="navbar-toggler-icon"></span>
          </button>
          <div class="collapse navbar-collapse justify-content-end " id="navbarNav">
            <ul class="navbar-nav">
              <li class="nav-item">
                <a class="nav-link active" aria-current="page" href="#">Home</a>
              </li>
              <li class="nav-item">
                <a class="nav-link" href="#profile">Profile</a>
              </li>
              <li class="nav-item">
                <a class="nav-link" href="#add&del">List & Delete</a>
              </li>
            </ul>
          </div>
        </div>
      </nav>
    </section>

    <!-- Banner -->
    <section class="container pt-5" id="#">
      <div class="row">
        <div class="col-lg-6">
          <h1 class="display-1 text-warning ">Portfolio</h1>
          <h5 class="display-5 text-secondary ">นาย วิลิตต์ กรกุลศรี</h5>
          <br><br>
        </div>
        <div class="col-lg-6 text-center shadow-sm"><img src="../src/img/ME.jpeg" alt="" height=500 width=430>
        </div>
      </div>
    </section>
  </div>
  <section class="container my-5 bg-light">
    <div class="row justify-content-center mt-3 py-3">
      <h1 class="col text-danger text-center" id="profile">Profile</h1>
    </div>
    <div class="row justify-content-center py-5">
      <div class="col-lg-3 col-md-6 col-sm-12">
        <div class="card">
          <img src="../src/img/Detail.png" class="card-img-top">
          <div class="card-body">
            <h5 class="card-title">My Details</h5>
            <p class="card-text">Name : นาย วิลิตต์ กรกุลศรี</p>
            <p class="card-text">Age : 21 </p>
            <p class="card-text">Studen ID : 6530200461 </p>
            <p class="card-text">Status : Study</p>
          </div>
        </div>
      </div>
      <div class="col-lg-3 col-md-6 col-sm-12">
        <div class="card">
          <img src="../src/img/hobby.jpg" class="card-img-top">
          <div class="card-body">
            <h5 class="card-title">Hobby</h5>
            <p class="card-text">ฟังเพลง เล่นเกม เขียนcode
              นอน ดูYoutube </p>
          </div>
        </div>
      </div>
      <div class="col-lg-3 col-md-6 col-sm-12">
        <div class="card">
          <img src="../src/img/Food.jpg" class="card-img-top">
          <div class="card-body">
            <h5 class="card-title">What i like ?</h5>
            <p class="card-text">Food : ข้าวหมูกระเทียม ข้าวผัดไข่</p>
            <p class="card-text">Desserts : ขนมปัง ขนมไทย</p>
          </div>
        </div>

      </div>
    </div>
  </section>

  <div class="container mt-5">
    <div class="m-2" id="add&del">
      <subAdd />
    </div>
    <div class="m-2" id="list">
      <subList />
    </div>
  </div>
</template>

<script>
import subList from './components/subList.vue';
import subAdd from './components/subAdd.vue';

export default {
  name: 'App',
  components: {
    subList,
    subAdd
  },
  data() {
    return {
      id: '01418214',
      name: 'Software Development',
      yr: '2023',
      sem: 2,
      secType: ['Lecture', 'Lab'],
      seat: 40,
      img: 'DB/12.jpeg',
      showAdd: false,
      showList: false
    }

  },
  methods: {
    toggleList() {
      this.showList = !this.showList
      this.showAdd = false
    },
    toggleAdd() {
      this.showAdd = !this.showAdd
      this.showList = false
    }
  }

}
window.onscroll = function () { scrollFunction() };

function scrollFunction() {
  if (document.body.scrollTop > 20 || document.documentElement.scrollTop > 20) {
    document.getElementById("navbar").style.top = "0";
  } else {
    document.getElementById("navbar").style.top = "-50px";
  }
}
</script>

<style>
#navbar {
  position: fixed;
  top: 0;
  width: 100%;
  z-index: 1000;
  /* ให้ navbar อยู่ด้านบนของเนื้อหา */
}
</style>
