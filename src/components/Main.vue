<template>
  <div class="hello">
    <div class=" text-center text-light" id="jumbotron">
      <div class="card-jumbo">
        <h1 class="display-4 text-warning">Motorcycle rental made easy</h1>
        <p class="lead ">Malaysia's first motorbike sharing. Insurance available for all!</p>
        <div class="row row-cols-lg-auto g-3 align-items-center justify-content-center">
          <div class="col-12">
            <label for="inlineFormSelectPref">Where</label>
            <select class="form-select" id="inlineFormSelectPref" v-mode="citySelected">
              <option v-for="city in cities" :key="city.id">{{city.name}}</option>
            </select>
          </div>
          <div class="col-12">
            <label for="inlineFormInputGroupUsername">Pick up date</label>
            <div class="input-group">
              <input type="date" class="form-control" id="inlineFormInputGroupUsername" placeholder="Pickup date" v-mode="pickupdate">
            </div>
          </div>
          <div class="col-12">
            <label for="inlineFormInputGroupUsername">Return date</label>
            <div class="input-group">
              <input type="date" class="form-control" id="inlineFormInputGroupUsername" placeholder="Pickup date" v-mode="returndate">
            </div>
          </div>

          <div class="col-12">
            <button type="submit" class="btn btn-primary" v-onclick="searchClick">Search</button>
          </div>
        </div>
      </div>
    </div>
    <section id="featured-bikers" class="py-5">
      <div class="container">
        <h3>Featured Bikes</h3>
        <div class="row">
          <div class="col-4" v-for="motor in motorbikes" :key="motor.name" v-on:click="detailClick(motor.id)">
            <div class="card">
              <img v-bind:src="motor.img" class="card-img-top" alt="...">
              <div class="card-body">
                <h5 class="card-title">{{motor.name}}</h5>
                <p class="card-text"><i class="fas fa-map-marker-alt"></i> {{motor.location}}</p>
              </div>
            </div>
          </div>
        </div>
      </div>

    </section>
    <section id="easy-rental" class="bg-warning py-5 text-center">
      <div class="container">
        <h3>Easy Motorcycle Rental</h3>
        <hr style="width:500px;margin:0 auto;" class="my-3">
        <div class="row">
          <div class="col-4">
            <h2 class="rental-icon"><i class="fas fa-search"></i></h2>
            <h5>Choose a Bike</h5><p>Over 110+ motorcycles listed! Rent the one that suits you.</p></div>
            <div class="col-4">
              <h2 class="rental-icon"><i class="fas fa-calendar-alt"></i></h2>
              <h5>Book your Trip</h5><p>Register your account, select bike and pay.</p></div>
              <div class="col-4">
                <h2 class="rental-icon"><i class="fas fa-motorcycle"></i></h2>
                <h5>Go for a Ride</h5><p>Protection options, insurance & unlimited kilometers.</p></div>
              </div>
            </div>
          </section>
          <section id="video" class="bg-light py-5 text-center">
            <h3>Learn about us</h3>
            <hr style="wideth:500px;margin:0 auto;" class="my-3">
            <iframe width="560" height="315" src="https://www.youtube.com/embed/UY0QY__2ESQ" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
          </section>
        </div>
      </template>

      <script>
      export default {
        name: 'Main',
        mounted(){
          console.log('page loaded!')
          let url = 'https://api.sheety.co/563fd43ab3cc2cabf5e64a5340870242/motors/sheet1';
          fetch(url)
          .then((response) => response.json())
          .then(json => {
  // Do something with the data
          this.motorbikes = (json.sheet1S);
        });
        },
        data(){
          return {
            motorbikes:[],
            cities : [
            {
              id:1,
              name:"Seremban"
            },
            {
              id:2,
              name:"Kuala Lumpur"
            },
            {
              id:3,
              name:"Melaka"
            },
            {
              id:4,
              name:"Perak"
            }
            ],

            pickupdate:'',
            returndate:'',
            citySelected:'Seremban'
          }
        },

        methods: {
          detailClick: function(id){
            console.log(id)
              this.$router.push({name:'Car',params:{id:id}})
          },
          searchClick: function(){

            this.$router.push({name:'Detail',params:{sendDate:this.pickupdate,returnDate:this.returndate,
              city:this.citySelected}})


               // window.location.href = "/detail/"+this.pickupdate+"/"+this.returndate+"/"+this.citySelected
             }
          // getImgUrl: function(url) {
          //  var images = require.context('../assets/', false, /\.jpg$/)
          //  return images( url )
        }


      }
      </script>

      <!-- Add "scoped" attribute to limit CSS to this component only -->
      <style scoped>

      #jumbotron {
        background-image:url('../../public/images/jumbos.jpg');
        background-size:cover;
        height: 80%;
        padding: 150px 0px;
      }
      .card-jumbo {
        border-radius: 15px;
        background-color: rgb(0,0,0,0.5);
        width: 60%;
        min-width:450px;
        margin: 0px auto;
        padding: 30px;
      }
      .rental-icon {
        font-size: 72px;
      }
      h3 {
        margin: 40px 0 0;
      }
      ul {
        list-style-type: none;
        padding: 0;
      }
      li {
        display: inline-block;
        margin: 0 10px;
      }
      a {
        color: #42b983;
      }
      </style>
