<template>
<q-page v-if="name !=null">
   <div style="padding:18% 0 0 0%; ">
      <img style=" margin-top:10%;"
      id="img"
      alt="Quasar logo"
      src="~assets/200.gif" class="window-width">
    </div>
  </q-page>
<q-page id="bg" v-else>
  <div>
  <div style="padding:18% 0 0 0%; ">
    <img style=" margin-top:0%;"
      id="img"
      alt="Quasar logo"
      src="~assets/f_view.jpg" class="window-width">
  </div>
  <transition
  v-if="show"
  appear
  :enter-active-class="anim"
  leave-active-class="animated fadeOut"
  >
  <div style="margin-top:%; padding-top:5%;" class="text-center">
    <img style="width:50%;"
      id="logo"
      alt="Quasar logo"
      src="~assets/logo.png">
  </div>
</transition>
</div>
</q-page>

</template>

<script>
const NAME = 'user_name';
export default {
  data(){
    return {
      name: localStorage.getItem(NAME),
      show:false,
      anim:'animated bounceInRight'
    }
  },
  methods:{
    sPage(){
      setTimeout(()=>this.$router.push('/s_view'), 5000)
    },
    vPage(){
      setTimeout(()=>this.$router.push('/viewer'), 2000)
    },
    removeCont(){
      setTimeout(()=>this.show=false, 5000)
    }
  },
  mounted(){
    if(this.name ==null){
    this.sPage();
    setTimeout(()=>this.show=true, 2000)
    // this.removeCont();
    }
    else{
    this.vPage();
    setTimeout(()=>this.show=true, 2000)
    }
    console.log(localStorage.getItem(NAME))
  }
}
</script>

<style>
  #bg{
      background-color:#683932;
      background-repeat: no-repeat;
      background-size: center;
  }
  #img{
    padding:3%;
    /* animation-name:img;
    animation-duration:10s; */
  }
  /* @keyframes img{
    0% { opacity:0.1}
    25% { opacity:0.7}
    50% { opacity:1.0}
    75% { opacity:1.1}
    100% { opacity:0.0}
  } */
    /* #logo{
    animation-name:logo;
    animation-duration:7s;
  } */
  /* @keyframes logo{
    0%    {opacity:0.1}
    25%   {opacity:0.7}
    50%   {opacity:1.0}
    75%   {opacity:1.1}
    100%  { opacity:0.0}
  } */
</style>
