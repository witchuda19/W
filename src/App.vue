<script setup>

import { ref } from 'vue';

const travel = ref("");
const money = ref(0);

// เก็บข้อมูลการจองร้าน
const bookinglist = ref([]);

// ข้อมูลการจองโต๊ะ
const bookingData = ref({
  name: "",
  phoneNumber: "",
  date: "",
  time: "",
  table:"",

});

// function สำหรับการจอง
function booking(restaurantName, data) {
  bookinglist.value.push({
    order: bookinglist.value.length + 1, // การจองลำดับที่
    name: data.name,
    restaurant: restaurantName,
    phoneNumber: data.phoneNumber,
    date: data.date,
    time: data.time,
    table: data.table
  });
  // ล้างข้อมูลหลังจากจอง
  bookingData.value = {
    name: "",
    phoneNumber: "",
    date: "",
    time: "",
    table: "",
  };
}

const travellist = ref ([
  {name:'ท่าช้าง',  img:"https://p-u.popcdn.net/event_details/posters/000/008/856/original/cfe1b94d03c5137faf1500f98117421e9f2ac9db.jpg?1590662796"},
  {name:'GoodView',  img:"https://th.bing.com/th/id/OIP.R9A5Gpn-DpOChTHyuic_sAHaFj?pid=ImgDet&rs=1"},
  {name:'RiverSide' ,  img:"https://th.bing.com/th/id/R.ab9802205edc889cdc62f84af245316c?rik=EUFmNFFfO91eJA&riu=http%3a%2f%2fwww.dooasia.com%2fwp-content%2fuploads%2f2018%2f05%2fThe-RiverSide-%e0%b9%80%e0%b8%8a%e0%b8%b5%e0%b8%a2%e0%b8%87%e0%b9%83%e0%b8%ab%e0%b8%a1%e0%b9%88-7-696x464.jpg&ehk=IfTrEAF8BEuE9hJhtMKHQNYZmV%2boSJEesY%2fzQmFNYoo%3d&risl=&pid=ImgRaw&r=0"},
  {name:'WarmUp',  img:"https://d136usn7jnoe61.cloudfront.net/pictures/21526/s2n_0002_p1d06tc4oou8jlkvr0l1mag1grj6.jpg"},
  {name:'ตะวันแดง',  img:"https://th.bing.com/th/id/R.6fd3de7109e6a325c0d72efb53de2050?rik=Aa1zQxZXAWtxSg&riu=http%3a%2f%2ftawandang.com%2fwp-content%2fuploads%2f2017%2f08%2fTWDjang-Chaeng-Wattana.jpg&ehk=WHcn32JlAx8ZTvDdAHwMb81EWoU%2fiVLDtNNd6K%2bP6Ao%3d&risl=&pid=ImgRaw&r=0"},
  {name:'Tamma',  img:"https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcRzc6gGgNTu5i89Zuk0jOm4-f9-swnyrOMuXw&usqp=CAU"},
]);

</script>

<template>

  <h1> 🍾🍻 Night cafe 🍷 </h1>

  <div class="p-3 m-0 border-0 bd-example m-0 border-0">
   <div class="text-center">
     <div class="row row-cols-1 row-cols-md-3 g-4">
       <div class="col" v-for="(i,name) in travellist" :key="index">
         <div class="card text-bg-dark h-100" style="width:18rem">
         <img v-if="i.img" :src="i.img" class="card-img-top" alt="..." />
         <div class="card-body">
         <h5 class="card-title">{{ i.name }}</h5>
          
          <a class="btn btn-primary" @click="booking(i.name, bookingData)">จองโต๊ะ</a>
         </div>
         </div>
       </div>
     </div>
   </div>
 </div>

 <div class="flex-container">
 <form class="row g-4">
 <div class="col-md-3">
   <label for="validationDefault01" class="form-label" style="color: #ffffff">ชื่อผู้จอง</label>
   <input type="text" v-model="bookingData.name" class="form-control" id="validationDefault01" required>
 </div> 

 <div class="col-md-3">
   <label for="validationDefault03" class="form-label" style="color: #ffffff">เบอร์โทร</label>
   <input type="text" v-model="bookingData.phoneNumber" class="form-control" id="validationDefault02" required>
 </div> 

 <div class="col-md-2">
  <label for="validationDefault03" class="form-label" style="color: #ffffff">เวลา</label>
  <input type="time" v-model="bookingData.time" class="form-control"  id="validationDefault03" required>
</div>


<div class="col-md-2">
  <label for="validationDefault03" class="form-label" style="color: #ffffff">จำนวนโต๊ะที่จอง</label>
  <input type="text" v-model="bookingData.table" class="form-control"  id="validationDefault03" required>
</div>


<div class="col-md-2">
 <label for="validationDefault03" class="form-label" style="color: #ffffff">จองโต๊ะวันที่</label>
  <input type="date" v-model="bookingData.date" class="form-control" id="validationDefault03" required>
</div>



</form>
</div>
 
<table class="table table-dark table-striped" v-if="bookinglist.length > 0">
  <thead>
    <tr>
      <th scope="col">#</th>
      <th scope="col">ชื่อผู้จอง</th>
      <th scope="col">ร้านที่จอง</th>
      <th scope="col">เบอร์โทรศัพท์</th>
      <th scope="col">วันที่จองโต๊ะ</th>
      <th scope="col">เวลา</th>
      <th scope="col">จำนวนโต๊ะที่จอง</th>
    </tr>
  </thead>
  <tbody>
    <tr v-for="(item, index) in bookinglist" :key="index">
      <th>{{ index + 1 }}</th>
      <td>{{ item.name }}</td>
      <td>{{ item.restaurant }}</td>
      <td>{{ item.phoneNumber }}</td>
      <td>{{ item.date }}</td>
      <td>{{ item.time }}</td>
      <td>{{ item.table }}</td>
      
    </tr>
  </tbody>
</table>



</template>

<style>
body {
  background: linear-gradient(to bottom, #001b7e, #ed006c,#1c1b4d);
}
.btn-primary {
  background-color: #4a0074; 
  border-color: #e2f0ff; 
  color: #fff; 
}
.flex-container {
    display: flex; 
    justify-content: space-around; 
    align-items: center; 
    border: 2px solid #ffffff; 
    padding: 10px; 
}
h1 {
    color: #FFA500; 
    font-size: 70px;
    text-shadow: 3px 3px 8px #ffdf86;
  }
</style>

