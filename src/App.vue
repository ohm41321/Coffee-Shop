<script setup>
  import{ ref } from "vue";

  const travel = ref("");
  const money = ref(0);

  const Details = ref({
    name: "",
    tel: "",
    date: "",
    time: "",
    tables: ""
  });
  
  //const travelList = ref(['Gunma','Shibuya','Akihabara','Kyoto','Fukuoka']);
  const travelList = ref([
    {name:'TeaCoff', price:80, size: {s:80, m: 150, l: 200}, img:"https://d1e00ek4ebabms.cloudfront.net/production/40075a8a-5e87-45fe-a24d-cc2e6d7738b6.jpg" },
    {name:'Coffee Guys', price: 50 , size: {s:50, m: 100, l: 150}, img:"https://okcredit-blog-images-prod.storage.googleapis.com/2021/05/Coffee---Tea-Shop1--1-.jpg" },
    {name:'Elegrant Tea', price: 90 , size: {s:90, m: 120, l: 150}, img:"https://static.wixstatic.com/media/d78afb_0a71705bbb6943269ad3d6b8e68e2959~mv2.jpg/v1/fill/w_640,h_294,al_c,q_80,usm_0.66_1.00_0.01,enc_auto/d78afb_0a71705bbb6943269ad3d6b8e68e2959~mv2.jpg" },
    {name:'Coffee Lab', price: 100 , size: {s:100, m: 150, l: 200}, img:"https://www.visitmesa.com/imager/s3_us-west-1_amazonaws_com/mesa-2019/images/Jarrods-Coffee-wide-view-3_6779f590680632ee6ed1060f38937405.jpg" },
    {name:'Two Tea', price: 30 , size: {s:30, m: 50, l: 100}, img:"https://rccl-h.assetsadobe.com/is/image/content/dam/royal/data/ship/spectrum/assets/renders/spectrum-of-the-seas-coffee-and-tea-shop.jpg?$750x420$" }, 
    {name:'Coffero', img:"https://mir-s3-cdn-cf.behance.net/project_modules/max_1200/e3539a49733633.58bd884b167cc.jpg"}
  ]);
  
  const bookingList = ref([
  ]);

  

  function booking(restaurant, details) {

  const bookingData = {
    restaurantName: restaurant.name,
    name: details.name,
    tel: details.tel,
    date: details.date,
    time: details.time,
    tables: details.tables,
  };
  
  bookingList.value.push(bookingData);

  Details.name = '';
  Details.tel = '';
  Details.date = '';
  Details.time = '';
  Details.tables = '';
  alert("Booking Complete!!! , Please Check Your Booking Details at The bottom of page")
}

  
  
//   //function
// function booking(name){
//   //name -> bookingList []
//   bookingList.value.push(name)
// }

</script>

<template>
  <h1 style="color: white ;">Select Your Favorite Restaurant</h1> <br>
  <div class="container-input" style="background-color: #5d7585;">
    <h4 style="color: rgb(245, 0, 0); font-weight: bold;">** กรุณากรอกข้อมูลให้ครบถ้วนก่อนจองโต๊ะ **</h4>
    <div class="cont">
          <div class="text-input">
            Name &nbsp; <input type="text" v-model="Details.name" required> 
          </div>
          <div class="text-input">
            Tel &nbsp; <input type="tel" v-model="Details.tel" required> 
          </div>
          <div class="text-input">  
            DD/MM/YYYY &nbsp; <input type="date" v-model="Details.date" required>
          </div>
          <div class="text-input">
            Time &nbsp; <input type="time" v-model="Details.time" required>
          </div>
          <div class="text-input">
            Tables &nbsp; <input type="number" v-model="Details.tables" required> 
          </div>
    </div>
  </div>
  <div class="container text-center" style="background-color: ; border-radius: 20px;">
    <div class="row" align="center">
      <div class="col" v-for="(item, index) in travelList" :key="index">
        <div class="card" style="width: 18rem; background-color: #7993a4; margin: 25px; border-radius: 30px;">
          <img :src="item.img" class="card-img-top" alt="...">
          <div class="card-body">
            <h5 class="card-title">{{ item.name }}</h5>
            <p class="card-text">Some quick example text.</p>
             <br>
            <a href="#" class="btn" @click="booking(item, Details)">จองโต๊ะ</a>
          </div>
        </div>
      </div>
    </div>
  </div> <br>
  <table class="table table-dark table-striped" v-if="bookingList.length > 0">
  <thead>
    <h4>Details</h4>
    <tr>
      <th scope="col">ชื่อร้าน</th>
      <th scope="col">ชื่อผู้จอง</th>
      <th scope="col">เบอร์โทร</th>
      <th scope="col">วัน/เดือน/ปี</th>
      <th scope="col">เวลา</th>
      <th scope="col">จำนวนโต๊ะ</th>
    </tr>
  </thead>
  <tbody>
    <tr v-for="(booking, index) in bookingList" :key="index">
      <td>{{ booking.restaurantName }}</td>
      <td>{{ booking.name }}</td>
      <td>{{ booking.tel }}</td>
      <td>{{ booking.date }}</td>
      <td>{{ booking.time }}</td>
      <td>{{ booking.tables }}</td>
    </tr>
  </tbody>
</table> <br>

  <div class="color">
    <h1>ไปเที่ยวกันมั้ย....</h1>
    <input type="radio" value="a" v-model="travel" />ภูเขา
    <input type="radio" value="b" v-model="travel" />ทะเล &nbsp;
    จำนวนเงิน &nbsp;
    <input type="number" v-model="money">
    <div v-if="money < 100">อยู่บ้านนอน</div>
    <div v-else-if="money >= 100 && money < 1000000">ขึ้นรถไปเที่ยว</div>
    <div v-else-if="money >= 1000000">ขับเครื่องบินส่วนตัวไป</div>
    <div v-else-if="money <= 0">กรุณากรอกจำนวนเงิน</div>
    <div v-if="travel === 'a' ">ภาพภูเขา</div>
    <div v-else>ภาพทะเล</div>
    <br>
    <button type="button" v-if="money < 50" disabled style="background-color: rgba(255, 0, 0, 0.142);">Let's Go</button>
    <button type="button" v-else style="background-color: green;">Let's Go</button>
  </div>
</template>
