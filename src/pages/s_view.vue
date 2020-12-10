<template>
<q-page id="bg" style="background-color:">
      <q-carousel
      animated
      id="caro"
      class="window-height"
      v-model="slide"
      navigation
      infinite
      :autoplay="autoplay"
      arrows
      transition-prev="slide-right"
      transition-next="slide-left"
      @mouseenter="autoplay = false"
      @mouseleave="autoplay = true"
    >
      <q-carousel-slide :name="1"  img-src="~assets/s_v_slide/one.png" />
      <q-carousel-slide :name="2"  img-src="~assets/s_v_slide/two.png" />
      <q-carousel-slide :name="3"  img-src="~assets/s_v_slide/three.png" />
      <q-carousel-slide :name="4"  img-src="~assets/s_v_slide/four.png" />
      <q-carousel-slide :name="5"  img-src="~assets/s_v_slide/five.png" />

    </q-carousel>
    <div style=" margin-top:-100px;">
    <center><q-btn label="let's get started" class="" @click="viewer"  color="primary"/></center>
    </div>
</q-page>
</template>

<script>
export default {
  data(){
    return{
      slide: 1,
      autoplay: true
    }
  },
  methods:{
    viewer(){
      this.$router.push('/viewer')
    }
  },
  mounted(){
  }
}
</script>

<style>
  /* #bg{
    /* background-color:'#37A000'; */
    /* background-color: rgba(0, 0, 0, 0.85); */
  /* } */

  #caro{
    padding:3%;
    /* animation-name:caro;
    animation-duration:5s; */
  }
  /* @keyframes caro{
    0%  {opacity:0.1}
    25% {opacity:0.3}
    50% {opacity:1.0}
    75% {opacity:1.1}
    100% { opacity:1.1}
  } */

  /* @media only screen and (max-height: 812px) { */
  /* For mobile phones: */
  /* [id*="caro"] {
    height: 812px;
    }
  } */

  /* @media only screen and (max-height: 640px) { */
  /* For mobile phones: */
  /* [id*="caro"] {
    height: 640px;
    }
  } */
</style>
