<template>
<q-pull-to-refresh @refresh="refresher">
  <!-- Content, whatever you like -->
  <q-page class="">
    <q-carousel
      swipeable
      animated
      v-model="slide"
      thumbnails
      infinite
      style="height:320px; padding-bottom:70px"
    >
      <q-carousel-slide :name="3" img-src="~assets/paslide/one.jpg" />
      <q-carousel-slide :name="2" img-src="~assets/paslide/two.jpg" />
      <q-carousel-slide :name="1" img-src="~assets/paslide/three.jpg" />
      <q-carousel-slide :name="4" img-src="~assets/paslide/four.jpg" />
      <q-carousel-slide :name="5" img-src="~assets/paslide/five.jpg" />
      <q-carousel-slide :name="6" img-src="~assets/paslide/six.jpg" />
      <q-carousel-slide :name="7" img-src="~assets/paslide/seven.jpg" />

      <!-- <template v-slot:control>
        <q-carousel-control
          position="bottom-right"
          :offset="[18, 18]"
        >
          <q-btn
            push round dense color="white" text-color="primary"
            :icon="fullscreen ? 'fullscreen_exit' : 'fullscreen'"
            @click="fullscreen = !fullscreen"
          />
        </q-carousel-control>
      </template> -->
    </q-carousel>

<!-- posts -->

<div class="q-pa-md" style="margin: 0px 0 20px 0">
    <div class="q-col-gutter-md row items-start">
      <div class="col-6">
        <q-img
          src="~assets/post6.jpg"
          style="width: 100%"
          v-model="post6"
          @click="post6=true"
        >
          <!-- <div class="absolute-bottom text-subtitle1 text-center">
            Caption
          </div> -->
        </q-img>
      </div>

      <div class="col-6">
        <q-img src="~assets/post4.jpg"
         v-model="post4"
          @click="post4=true">
        </q-img>
      </div>
      </div>

          <div class="q-col-gutter-md row items-start">
      <div class="col-6">
        <q-img
          src="~assets/post3.jpg"
          style="width: 100%"
           v-model="post3"
          @click="post3=true"
        >
        </q-img>
      </div>

      <div class="col-6">
        <q-img src="~assets/post2.jpg"
         v-model="post2"
          @click="post2=true">
        </q-img>
      </div>
      </div>
      <div class="flex flex-center">
    <img style="width:100%; margin-top:;"
      alt="Quasar logo"
      src="~assets/post1.jpg"
    >
</div>
    </div>

      <q-dialog v-model="alert">
      <q-card>
        <q-card-section>
          <div class="text-h6">Disclaimer: </div>
        </q-card-section>

        <q-card-section class="q-pt-none">
          Kindly Note that, the hospital will not be held responsible for any
          action done with this account after login as your supposed to protect your login details at
           all time
        </q-card-section>

        <q-card-actions align="right">
          <q-btn flat label="ACCEPT" color="primary" v-close-popup />
        </q-card-actions>
      </q-card>
    </q-dialog>

<!-- full post -->
    <q-dialog v-model="post6">
<q-card-section class="row" style="background-color:white;">
          <q-space/>
          <q-btn
          v-close-popup
          icon="close"
          />
<div class="flex flex-center">
    <img style="width:100%; margin-top:;"
      alt="Quasar logo"
      src="~assets/post6.jpg"
    >
</div>

</q-card-section>
</q-dialog>
<q-dialog v-model="post4">
        <q-card-section class="row" style="background-color:white;">
          <q-space/>
          <q-btn
          v-close-popup
          icon="close"
          />
<div class="flex flex-center">
    <img style="width:100%; margin-top:;"
      alt="Quasar logo"
      src="~assets/post4.jpg"
    >
</div>

</q-card-section>
</q-dialog>
<q-dialog v-model="post3">
        <q-card-section class="row" style="background-color:white;">
          <q-space/>
          <q-btn
          v-close-popup
          icon="close"
          />
<div class="flex flex-center">
    <img style="width:100%; margin-top:;"
      alt="Quasar logo"
      src="~assets/post3.jpg"
    >
</div>

</q-card-section>
</q-dialog>
<q-dialog v-model="post2">
        <q-card-section class="row" style="background-color:white;">
          <q-space/>
          <q-btn
          v-close-popup
          icon="close"
          />
<div class="flex flex-center">
    <img style="width:100%; margin-top:;"
      alt="Quasar logo"
      src="~assets/post2.jpg"
    >
</div>

</q-card-section>
</q-dialog>
  </q-page>
</q-pull-to-refresh>

</template>

<script>
const NAME = 'user_name';

export default {
  name: 'PageIndex',
  data () {
    return {
      alert: true,
      slide: 1,
      post6 : false,
      post4 : false,
      post3 : false,
      post2 : false,
      fullscreen: false
    }
  },
mounted(){
      setTimeout(this.$forceUpdate(), 5000)

  },
methods:{
      methodThatForcesUpdate() {
      // ...
       // Notice we have to use a $ here
      // ...
    },
  // window.location.reload()
    refresher (done) {
    this.$router.go(this.$router.currentRoute)

},
  toUsers(){
    this.$router.push('/users')
  },
  toDocs(){
    this.$router.push('/doc')
  }
}
}
</script>
