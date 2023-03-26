<template >
  <div>
    <Navbar></Navbar>
       <section id="product1" class="section-p1">
      <h2>Featured Products</h2>
      <p>Summer Collection New Modern Design</p>
      <div class="pro-container" >
        <div class="pro" v-for="(shoe, index) in shoes" :key="index">
          <img :src="shoe.image" alt="" />
          <div class="des">
            <span>Nike</span>
            <h5>{{ shoe.title }}</h5>
            <div class="star">
              <i class="fa fa-star"></i>
              <i class="fa fa-star"></i>
              <i class="fa fa-star"></i>
              <i class="fa fa-star"></i>
              <i class="fa fa-star"></i>
            </div>
            <h4>
              {{
              new Intl.NumberFormat("Rp", {
                style: "currency",
                currency: "idr",
              }).format(Math.round(shoe.price))
            }}
            </h4>
          </div>
          <nuxt-link
            tag="button"
            :to="{ path: 'details', query: { shoes: shoe } }"
            >Details</nuxt-link
          >
        </div>
      </div>
    </section>
        <Footer></Footer>
  </div>
</template>
<script>
import Navbar from "../components/Navbar.vue"
import Footer from "../components/Footer.vue";
import axios from "axios";
export default {
  name: "IndexPage",
  data() {
    return {
      // shoes: [],
    };
  },
  middleware: ["check-auth", "auth"],
  components: {
    Navbar,
    Footer,
  },
  async asyncData() {
    const shoes = [];
    const post = await axios
      .get("https://vue-js-project-3ebb3-default-rtdb.firebaseio.com/shoeList.json")
      .then((response) => {
        for (const key in response.data) {
          shoes.push({ ...response.data[key], id: key });
        }
      });
    return { shoes };
  },
}
</script>
<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: sans-serif;
}

h1 {
  font-size: 50px;
  line-height: 64px;
  color: #222;
}

h2 {
  font-size: 46px;
  line-height: 54px;
  color: #222;
}

h4 {
  font-size: 20px;
  color: #222;
}

h6 {
  font-weight: 700;
  font-size: 12px;
}

p {
  font-size: 16px;
  color: #465b52;
  margin: 15px 0 20px 0;
}

.section-p1 {
  padding: 40px 80px;
}

.section-m1 {
  margin: 40px 0;
}

#banner button {
  height: 45px;
  width: 150px;
  font-size: 14px;
  font-weight: 600;
  padding: 15 30px;
  color: #000;
  background-color: #fff;
  border-radius: 4px;
  cursor: pointer;
  border: none;
  outline: none;
  transition: 0.2s;
}

body {
  width: 100%;
}

img,
.logo {
  width: 70px;
  height: 40px;
}

#hero h4 {
  padding-bottom: 15px;
}

#hero h1 {
  color: #088178;
}

#hero button,
image {
  background-image: url("https://th.bing.com/th/id/R.fdd6ecca83cedc5ffd4c9a713e451361?rik=EZhnIXZe9Us33A&riu=http%3a%2f%2fhealthwebcart.com%2fwp-content%2fuploads%2f2021%2f05%2fshop.png&ehk=jQWNEbF026MvctpjVmtEFFUUFI4EcPIXb4CBZ6ezAOA%3d&risl=&pid=ImgRaw&r=0");
  background-size: cover;
  height: 65px;
  width: 200px;
  padding: 14px 80px 14px 65px;
  background-repeat: no-repeat;
  cursor: pointer;
}

#feature {
  display: flex;
  align-items: center;
  justify-content: space-between;
  flex-wrap: wrap;
}

#feature .fe-box {
  width: 180px;
  text-align: center;
  padding: 25px 15px;
  box-shadow: 20px 20px 34px rgba(0, 0, 0, 0.03);
  border: 1px solid #cce7d0;
  border-radius: 4px;
  margin: 15px 0;
}

#feature .fe-box:hover {
  box-shadow: 10px 10px 54px rgba(70, 62, 221, 0.1);
}

#feature .fe-box img {
  margin-bottom: 10px;
  height: 80px;
}

#feature .fe-box h6 {
  display: inline-block;
  padding: 9px 8px 6px 8px;
  line-height: 1;
  border-radius: 4px;
  color: #088178;
  background-color: lightcyan;
}

#product1 {
  text-align: center;
}

.pro-container {
  display: flex;
  justify-content: space-between;
  padding-top: 20px;
  flex-wrap: wrap;
}

#product1 .pro {
  width: 23%;
  min-width: 250px;
  padding: 10px 12px;
  border: 1px solid #cce7d0;
  border-radius: 25px;
  cursor: pointer;
  box-shadow: 20px 20px 30px rgba(0, 0, 0, 0.02);
  margin: 15px 0;
  transition: 0.2s ease;
  position: relative;
}

#product1 .pro:hover {
  box-shadow: 20px 20px 30px rgba(0, 0, 0, 0.06);
}

#product1 .pro img {
  width: 100%;
  height: 150px;
  border-radius: 20px;
}

#product1 .pro .des {
  text-align: start;
  padding: 10px 0;
}

#product1 .pro .des span {
  color: #606063;
  font-size: 12px;
}

#product1 .pro .des h5 {
  padding-top: 7px;
  color: #1a1a1a;
  font-size: 14px;
}

#product1 .pro .des i {
  font-size: 12px;
  color: rgb(243, 181, 25);
}

#product1 .pro .des h4 {
  padding-top: 7px;
  font-size: 15px;
  font-weight: 700;
  color: #088178;
}

#product1 .pro .cart {
  width: 40px;
  height: 40px;
  line-height: 40px;
  border-radius: 50px;
  background-image: url("https://th.bing.com/th/id/R.f449e5b2eaed9cf43c7697bceb7674b8?rik=QceMFLO6IjguOQ&riu=http%3a%2f%2fwww.clipartbest.com%2fcliparts%2fdTr%2f6a7%2fdTr6a7K8c.png&ehk=bnZDAxhtSRZMi9Tj56wsz%2fmW7DBXJzAam9PgMT0fw5o%3d&risl=&pid=ImgRaw&r=0");
  background-size: cover;
  background-color: #e8f6ea;
  position: absolute;
  bottom: 20px;
  right: 10px;
}

#banner {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  text-align: center;
  background-image: url("https://t1.daumcdn.net/cfile/blog/2739D34755BC547E31");
  background-size: cover;
  width: 100%;
  height: 40vh;
  background-position: center;
}

#banner h4 {
  color: #fff;
  font-size: 20px;
}

#banner h2 {
  color: #fff;
  font-size: 40px;
  padding: 10px 0;
}

#banner h2 span {
  color: #fff;
  font-weight: bold;
}

#banner button:hover {
  background: #088178;
  color: #fff;
}

#sm-banner {
  display: flex;
  justify-content: space-between;
  flex-wrap: wrap;
}

#sm-banner .banner-box {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: flex-start;
  background-image: url("https://wallpapercave.com/wp/wp2557389.jpg");
  background-size: cover;
  min-width: 550px;
  height: 50vh;
  background-position: center;
  color: #fff;
  padding: 30px;
}

#sm-banner .banner-box2 {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: flex-start;
  background-image: url("https://flightactionsports.com/wp-content/uploads/2014/04/slider.png");
  background-size: cover;
  min-width: 550px;
  height: 50vh;
  background-position: center;
  color: #fff;
  padding: 30px;
}

#sm-banner .banner-box h4 {
  color: #fff;
  font-size: 20px;
  font-weight: 300;
}

#sm-banner .banner-box h2 {
  color: #fff;
  font-size: 28px;
  font-weight: 800;
}

#sm-banner .banner-box span {
  color: #fff;
  font-size: 14px;
  font-weight: 500;
  padding-bottom: 15px;
}

#sm-banner .white {
  height: 45px;
  width: 150px;
  font-size: 13px;
  font-weight: 600;
  padding: 11 18px;
  color: #fff;
  background-color: transparent;
  cursor: pointer;
  border: 1 px solid #fff;
  outline: none;
  transition: 0.2s;
}

#sm-banner .white:hover {
  background: #088178;
  border: 1px solid #088178;
}

#sm-banner .banner-box2 h4 {
  color: #fff;
  font-size: 20px;
  font-weight: 300;
}

#sm-banner .banner-box2 h2 {
  color: #fff;
  font-size: 28px;
  font-weight: 800;
}

#sm-banner .banner-box2 span {
  color: #fff;
  font-size: 14px;
  font-weight: 500;
  padding-bottom: 15px;
}

#banner3 .banner-box {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: flex-start;
  background-image: url("https://th.bing.com/th/id/R.4628c7d9b6b20b1c0c7c8edbb7a6ffb0?rik=FTInYEvxdWUHIw&riu=http%3a%2f%2fwww.sneakerfiles.com%2fwp-content%2fuploads%2f2015%2f06%2fnike-kd-7-elite-rose-gold-detailed-6.jpg&ehk=759Ex2XHdCgtOT5x9reSu8tMgC0jWykr7KWHi3pwSQo%3d&risl=&pid=ImgRaw&r=0");
  background-size: cover;
  min-width: 330px;
  height: 30vh;
  background-position: center;
  color: #fff;
  padding: 20px;
  margin-bottom: 20px;
}

#banner3 .banner-box4 {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: flex-start;
  background-image: url("https://th.bing.com/th/id/R.a2aa1d3102b43f5f16592dd2610a7308?rik=SwyHWBgX%2f7cTzA&riu=http%3a%2f%2fwww2.flightclub.cn%2fnews%2fuploads%2fallimg%2f161020%2f7-1610201SI8.jpg&ehk=L5C0Mn%2fDPoX2AMslMOnnKWhKCZ7FqgQJkv8V9pegJgc%3d&risl=&pid=ImgRaw&r=0");
  background-size: cover;
  min-width: 330px;
  height: 30vh;
  background-position: center;
  color: #fff;
  padding: 20px;
  margin-bottom: 20px;
}

#banner3 .banner-box5 {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: flex-start;
  background-image: url("https://www.cleveland.com/resizer/xQYCuQoJZ6v79-y620bYvtB_-Ak=/450x0/smart/cloudfront-us-east-1.images.arcpublishing.com/advancelocal/SVSBPD4WRNAIBGOQSWYNEP6PZM.jpg");
  background-size: cover;
  min-width: 330px;
  height: 30vh;
  background-position: center;
  color: #fff;
  padding: 20px;
  margin-bottom: 20px;
}

#banner3 .banner-box h2 {
  color: #fff;
  font-weight: 900;
  font-size: 22px;
}

#banner3 .banner-box h3 {
  color: #fff;
  font-weight: 800;
  font-size: 15px;
}

#banner3 {
  display: flex;
  justify-content: space-between;
  flex-wrap: wrap;
  padding: 0 80px;
}

#banner3 .banner-box4 h2 {
  color: #fff;
  font-weight: 900;
  font-size: 22px;
}

#banner3 .banner-box4 h3 {
  color: #fff;
  font-weight: 800;
  font-size: 15px;
}

#banner3 .banner-box5 h2 {
  color: #fff;
  font-weight: 900;
  font-size: 22px;
}

#banner3 .banner-box5 h3 {
  color: #fff;
  font-weight: 800;
  font-size: 15px;
}

#newsletter {
  display: flex;
  justify-content: space-between;
  flex-wrap: wrap;
  align-items: center;
  background-image: url("https://th.bing.com/th/id/R.8a1cbaa2e04b77fead30559e91a29bc5?rik=TAe%2bf6WhC1anyQ&riu=http%3a%2f%2fwww.pixelstalk.net%2fwp-content%2fuploads%2f2016%2f08%2fHD-free-black-wallpaper.jpg&ehk=WrolQy%2bhkhUTDMZIdR1JlcQb%2bqPubiPfLwxeRyRlmGY%3d&risl=&pid=ImgRaw&r=0");
  background-size: cover;
  background-repeat: no-repeat;
  background-position: 20% 30%;
}

#newsletter h4 {
  font-size: 22px;
  font-weight: 700;
  color: #fff;
}

#newsletter p {
  font-size: 14px;
  font-weight: 600;
  color: #818ea0;
}

#newsletter p span {
  color: #088178;
}

#newsletter .form {
  display: flex;
  width: 40%;
}

#newsletter input {
  height: 3.125rem;
  padding: 0 1.25em;
  font-size: 14px;
  width: 100%;
  border: 1px solid transparent;
  border-radius: 4px;
  outline: none;
  border-top-right-radius: 0;
  border-bottom-right-radius: 0;
}

#newsletter button {
  height: 3.125rem;
  width: 150px;
  font-size: 14px;
  font-weight: 600;
  padding: 15 30px;
  color: #fff;
  background-color: #088178;
  white-space: nowrap;
  border-radius: 4px;
  cursor: pointer;
  border: none;
  outline: none;
  transition: 0.2s;
  border-top-left-radius: 0;
  border-bottom-left-radius: 0;
}

footer {
  display: flex;
  justify-content: space-between;
  flex-wrap: wrap;
  background-color: #e3e6f3;
}

footer .col {
  display: flex;
  flex-direction: column;
  align-items: flex-start;
  margin-bottom: 20px;
}

footer .logo {
  margin-bottom: 30px;
}

footer h4 {
  font-size: 14px;
  padding-bottom: 20px;
}

footer p {
  font-size: 13px;
  margin: 0 0 8px 0;
}

footer a {
  font-size: 13px;
  text-decoration: none;
  color: #222;
  margin-bottom: 10px;
}

footer .follow {
  margin-top: 20px;
}

footer .follow {
  margin-top: 20px;
}

footer .follow img {
  width: 20px;
  height: 20px;
}

footer .row img {
  width: 330px;
  height: 110px;
  border: 1px solid #088178;
  padding: 6px 6px 6px 6px;
  border-radius: 6px;
  margin-bottom: 10px;
}

footer .payment img {
  width: 80px;
  height: 40px;
  margin: 10px 0 15px 0;
}

footer .col a:hover {
  color: #088178;
}

footer .copyright {
  width: 100%;
  text-align: center;
}

#page-header {
  background-image: url("https://i.pinimg.com/originals/0c/ca/56/0cca5686837cb07b4b7778a0b332bc61.jpg");
  width: 100%;
  height: 40vh;
  background-size: cover;
  display: flex;
  justify-content: center;
  text-align: center;
  flex-direction: column;
  padding: 14px;
}

#page-header h2,
#page-header p {
  color: #fff;
}

#pagination {
  text-align: center;
}

#pagination a {
  text-decoration: none;
  background-color: #088178;
  padding: 15px 20px;
  border-radius: 4px;
  color: #fff;
  font-weight: 600;
}

#prodetails .single-pro-image {
  width: 47%;
  margin-right: 15px;
}

#prodetails .single {
  width: 500px;
  height: 320px;
}

.small-img-group {
  display: flex;
  justify-content: space-between;
}

.small-img-col {
  flex-basis: 24%;
  cursor: pointer;
}

#prodetails {
  display: flex;
  margin-top: 20px;
}

#prodetails .single-pro-details {
  width: 50%;
  padding-top: 30px;
}

#prodetails .single-pro-details h4 {
  padding: 40px 0 20px 0;
}

#prodetails .single-pro-details h2 {
  font-size: 26px;
}

#prodetails .single-pro-details select {
  display: block;
  padding: 5px 10px;
  margin-bottom: 10px;
}

#prodetails .single-pro-details input {
  width: 50px;
  height: 47px;
  padding-left: 10px;
  font-size: 16px;
  margin-right: 10px;
}

#prodetails .single-pro-details input:focus {
  outline: none;
}

#prodetails .single-pro-details button {
  background: #088178;
  color: #fff;
  height: 3.125rem;
  width: 150px;
  font-size: 14px;
  font-weight: 600;
  padding: 15 30px;
  white-space: nowrap;
  border-radius: 4px;
  cursor: pointer;
  border: none;
  outline: none;
  transition: 0.2s;
}

#prodetails .single-pro-details span {
  font-size: 20px;
  font-weight: 600;
}

#page-header .blog-header {
  background-image: url("https://i.pinimg.com/originals/d1/7c/c3/d17cc380dbcc9534b83e4014f577cc54.jpg");
  width: 100%;
  height: 40vh;
  background-size: cover;
  display: flex;
  justify-content: center;
  text-align: center;
  flex-direction: column;
  padding: 14px;
}

#blog {
  padding: 150px 150px 0 150px;
}

#blog .blog-box {
  display: flex;
  align-items: center;
  width: 100%;
  position: relative;
  padding-bottom: 90px;
}

#blog .blog-img {
  width: 100%;
  margin-right: 40px;
}

#blog img {
  width: 100%;
  height: 300px;
  object-fit: cover;
}

#blog .blog-details {
  width: 50%;
}

#blog .blog-details a {
  text-decoration: none;
  font-size: 11px;
  color: #000;
  font-weight: 700;
  position: relative;
  transition: 0.3s;
}

#blog .blog-details a::after {
  content: "";
  width: 50px;
  height: 1px;
  background-color: #000;
  position: absolute;
  top: 4px;
  right: -60px;
}

#blog .blog-details a:hover {
  color: #088178;
}

#blog .blog-details a:hover::after {
  background-color: #088178;
}

#blog .blog-box h1 {
  position: absolute;
  top: -40px;
  left: 0;
  font-size: 70px;
  font-weight: 700;
  color: #c9cbce;
  z-index: -9;
}

#page-header .about-header {
  background-image: url("https://th.bing.com/th/id/R.44f10d58ad8d5160b8c99d6fb9019a35?rik=dJBz%2bMLpvf%2fpPA&riu=http%3a%2f%2fwww.pixelstalk.net%2fwp-content%2fuploads%2f2016%2f10%2fAesthetic-Pictures.jpg&ehk=%2fnhhQJo%2bMQQLHd4S4pNFbCVmBiTvpUIA20Qf64L3O1k%3d&risl=&pid=ImgRaw&r=0");
  width: 100%;
  height: 40vh;
  background-size: cover;
  display: flex;
  justify-content: center;
  text-align: center;
  flex-direction: column;
  padding: 14px;
}

#about-head {
  display: flex;
  align-items: center;
}

#about-head img {
  width: 400px;
  height: auto;
}

#about-head div {
  padding-left: 40px;
}

#about-app {
  text-align: center;
}

#about-app .video {
  width: 70%;
  height: 100%;
  margin: 30px auto 0 auto;
}

#about-app img {
  width: 100%;
  height: 100%;
  border-radius: 20px;
}

#contact-details {
  display: flex;
  align-items: center;
  justify-content: space-between;
}

#contact-details .details {
  width: 40%;
}

#contact-details .details span,
#form-details form span {
  font-size: 12px;
}

#contact-details .details h2,
#form-details form h2 {
  font-size: 16px;
  padding-bottom: 15px;
}

#contact-details .details li {
  list-style: none;
  display: flex;
  padding: 10px 0;
}

#contact-details .details li img {
  width: 20px;
  height: 20px;
}

#contact-details .details li p {
  margin: 0;
  font-size: 14px;
  padding-left: 22px;
}

#contact-details .map {
  width: 55%;
  height: 400px;
}

#contact-details .map iframe {
  width: 100%;
  height: 100%;
}

#form-details {
  display: flex;
  justify-content: space-between;
  margin: 30px;
  padding: 80px;
  border: 1px solid #e1e1e1;
}

#form-details form {
  width: 65%;
  display: flex;
  flex-direction: column;
  align-items: flex-start;
}

#form-details form input,
#form-details form textarea {
  width: 100%;
  padding: 12px 15px;
  outline: none;
  margin-bottom: 20px;
  border: 1px solid #e1e1e1;
}

#form-details form button {
  background: #088178;
  color: #fff;
  height: 3.125rem;
  width: 150px;
  font-size: 14px;
  font-weight: 600;
  padding: 15px 30px;
  margin-left: 20px;
  white-space: nowrap;
  border-radius: 4px;
  cursor: pointer;
  border: none;
  outline: none;
  transition: 0.2s;
}

#form-details .people div {
  padding-bottom: 25px;
  display: flex;
  align-items: flex-start;
}

#form-details .people div img {
  width: 65px;
  height: 65px;
  object-fit: cover;
  margin-right: 15px;
}

#form-details .people div p {
  margin: 0;
  font-size: 13px;
  line-height: 25px;
}

#form-details .people div p span {
  display: block;
  font-size: 16px;
  font-weight: 600;
  color: #000;
}

#cart table {
  width: 100%;
  border-collapse: collapse;
  table-layout: fixed;
  white-space: nowrap;
}

#cart table img {
  width: 90px;
  height: 50px;
}

#cart table td:nth-child(1) {
  width: 100px;
  text-align: center;
}

#cart table td:nth-child(2) {
  width: 150px;
  text-align: center;
}

#cart table td:nth-child(3) {
  width: 250px;
  text-align: center;
}

#cart table td:nth-child(4),
#cart table td:nth-child(5),
#cart table td:nth-child(6) {
  width: 100px;
  text-align: center;
}

#cart table td:nth-child(5) input {
  width: 70px;
  padding: 10px 5px 10px 15px;
}

#cart table thead {
  border: 1px solid #e2e9e1;
  border-left: none;
  border-right: none;
}

#cart table thead td {
  font-weight: 700;
  text-transform: uppercase;
  font-size: 13px;
  padding: 18px 0;
}

#cart table tbody tr td {
  padding-top: 15px;
}

#cart table tbody td {
  font-size: 13px;
}
</style>
