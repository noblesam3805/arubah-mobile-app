<template>
  <q-page class="" id="bg">

    <div class="" style="margin-top:0px">
    <!-- <q-carousel
      v-model="slide"
      transition-prev="slide-right"
      transition-next="slide-left"
      swipeable
      animated
      control-color="primary"
      navigation
      autoplay
      padding
      height="300px"
      class="bg-grey-1 shadow-2 rounded-borders"
    >
      <q-carousel-slide :name="1" class="column no-wrap">
        <div class=" fit justify-start items-center q-gutter-xs q-col-gutter no-wrap">
          <q-img class="rounded-borders col-6 full-height" src="~assets/v_slide/fourrr.jpg" />
        </div>
      </q-carousel-slide>
      <q-carousel-slide :name="2" class="column no-wrap">
        <div class=" fit justify-start items-center q-gutter-xs q-col-gutter no-wrap">
          <q-img class="rounded-borders col-6 full-height" src="~assets/v_slide/threeee.jpg" />
        </div>
      </q-carousel-slide>
      <q-carousel-slide :name="3" class="column no-wrap">
        <div class=" fit justify-start items-center q-gutter-xs q-col-gutter no-wrap">
          <q-img class="rounded-borders col-6 full-height" src="~assets/v_slide/viewer.jpg" />
        </div>
      </q-carousel-slide>

    </q-carousel> -->
  </div>

    <div style="padding:85% 0 100px 0px;" class="text-center">
    <div class="row text-center" style="margin-left:">
      <q-btn color="primary" style="margin:auto;height:100px; width:40%" class="" label="our clinics" stack icon-right="trending_up"  @click="number = true"/>
      <q-btn color="primary" style="margin:auto;height:100px; width:40%" class="" label="clinic time" stack icon-right="alarm"  @click="time = true"/>
    </div>
    <div class="row text-center" style="margin-top:10px; margin-left:">
    <q-btn color="primary" style="margin:auto; height:100px; width:40%" class="" label="about us" stack icon-right="speaker_notes"  @click="faq = true"/>
    <q-btn color="primary" style="margin:auto; height:100px; width:40%" label="contact us" class="" stack icon-right="contact_phone"  @click="contact=true"/>
    </div>
    </div>


<!-- posts -->
<!--<div class="q-pa-md" style="margin: 40px 0 20px 0">
      <div class="q-col-gutter-md row items-start">
       <div class="col-6">
        <q-img
          src="~assets/post6.jpg"
          style="width: 100%"
          v-model="post6"
          @click="post6=true"
        >
           <div class="absolute-bottom text-subtitle1 text-center">
            Caption
          </div>
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
    </div> -->
  <!-- dialog section frequent questions -->
  <q-dialog v-model="faq" id="bgt">
        <q-card-section  class="row" style="color:white;">
          <div class="text-h6" style="color:white;">About The Hospital</div>
          <q-space/>
          <q-btn
          v-close-popup
          icon="close"
  />
<q-list  bordered style="margin-top:6%;">

<q-item class="p-md-a">
<div class="row">
  <div class="column">
    <q-item-section>
          <q-item-label
          class="q-pa-md" style="text-align:justify" >
           <p>ARUBAH SPECIALIST HOSPITAL has been around for five years and at all times been a symbol of hope and comfort for all those we come in contact with. Our Ultimate goal is captured succinctly in our mission: “Committed to the restoration to full Health of our patients using our skills, equipment and faith
              in GOD and at all times show compassion and love to all that we come in contact with”. </p>
            <p>
We have met the requirements stated for Health Care Providers and we are among the best in the medical
industry with regards to the provision of both primary and secondary healthcare services. </p>
<p>
Due to the optimum standard we have kept since inception, we have been accredited by the National Health Insurance Scheme (NHIS CODE: CR/0159/P) as
 a provider for both primary and secondary care for everyone registered under the scheme. </p>
 <div>
  <div>
    <p>Since its founding we become an integral part of the city,   advancing
      our mission of providing access to compassionate care to our   communities. Today patients find care that combines world-class medicine   with compassion.</p>
  </div>
</div>

          </q-item-label>
        </q-item-section>
        <!-- <q-item-section class="q-ml-md">
          <q-item-label caption >
         <b>lorem ipsum frem dolor de caker nar trun</b>
          </q-item-label>
        </q-item-section> -->
  </div>
</div>
</q-item>
</q-list>
        </q-card-section>
</q-dialog>

  <!-- dialog section full posts -->
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

  <!-- dialog second section full posts -->
<q-dialog v-model="post7">
<q-card-section class="row" style="background-color:white;">
          <q-space/>
          <q-btn
          v-close-popup
          icon="close"
          />
<div class="flex flex-center">
    <img style="width:100%; margin-top:;"
      alt="Quasar logo"
      src="~assets/post7.jpg"
    >
</div>

</q-card-section>
</q-dialog>
<q-dialog v-model="post8">
        <q-card-section class="row" style="background-color:white;">
          <q-space/>
          <q-btn
          v-close-popup
          icon="close"
          />
<div class="flex flex-center">
    <img style="width:100%; margin-top:;"
      alt="Quasar logo"
      src="~assets/post8.jpg"
    >
</div>

</q-card-section>
</q-dialog>
<q-dialog v-model="post9">
        <q-card-section class="row" style="background-color:white;">
          <q-space/>
          <q-btn
          v-close-popup
          icon="close"
          />
<div class="flex flex-center">
    <img style="width:100%; margin-top:;"
      alt="Quasar logo"
      src="~assets/post9.jpg"
    >
</div>

</q-card-section>
</q-dialog>
<q-dialog v-model="post10">
        <q-card-section class="row" style="background-color:white;">
          <q-space/>
          <q-btn
          v-close-popup
          icon="close"
          />
<div class="flex flex-center">
    <img style="width:100%; margin-top:;"
      alt="Quasar logo"
      src="~assets/post10.jpg"
    >
</div>

</q-card-section>
</q-dialog>


  <!-- dialog section time -->
    <q-dialog v-model="time" id="bgs">
      <q-card-section class="row" style="">
          <div class="text-h6"  style="color:white;">Clinic Time</div>
          <q-space/>
          <q-btn
          v-close-popup
          icon="close"
          style="color:white"
          />

      <div class="q-pa-md q-ma-md" style="margin:40px 0 0 0;width:100%;color:white;">
    <q-list style="font-size:20px">
      <q-item>
        <q-item-section>
          <q-item-label style="color:#F5FD0D;">Mondays</q-item-label>
          <q-item-label caption lines="2" style="color:white;font-size:16px">
            <b>Radiology Clinic
            (4D Ultra sound services)
            , Main Branch, Marian</b></q-item-label>
        </q-item-section>

        <q-item-section side top>
          <q-item-label caption style="color:white;font-size:16px"><b>9 AM</b></q-item-label>
          <q-icon name="alarm" color="secondary" />
        </q-item-section>
      </q-item>

      <q-item>
        <q-item-section>
          <q-item-label style="color:#F5FD0D;">Tuesdays</q-item-label>
          <q-item-label caption lines="2" style="color:white; font-size:16px">
            <b>Ophthalmologist and Optometrists Clinic
, Annex(Satellite town Branch)</b></q-item-label>
        </q-item-section>

        <q-item-section side top>
          <q-item-label caption style="color:white;font-size:16px"><b>2 PM</b></q-item-label>
          <q-icon name="alarm" color="secondary" />
        </q-item-section>
      </q-item>

      <q-item>
        <q-item-section>
          <q-item-label caption lines="2" style="color:white;font-size:16px">
           <b>Pediatrics Clinic
, Main Branch, Marian</b></q-item-label>
        </q-item-section>

        <q-item-section side top>
          <q-item-label caption style="color:white;font-size:16px"><b>4 PM</b></q-item-label>
          <q-icon name="alarm" color="secondary" />
        </q-item-section>
      </q-item>

      <q-item>
        <q-item-section>
          <q-item-label caption lines="2" style="color:white;font-size:16px">
           <b>Cardiologist Clinic
, Main Branch, Marian</b></q-item-label>
        </q-item-section>

        <q-item-section side top>
          <q-item-label caption style="color:white;font-size:16px"><b>5 PM</b></q-item-label>
          <q-icon name="alarm" color="secondary" />
        </q-item-section>
      </q-item>

      <q-item>
        <q-item-section>
          <q-item-label caption lines="2" style="color:white;font-size:16px">
           <b>Physician Clinic
, Main Branch, Marian</b></q-item-label>
        </q-item-section>

        <q-item-section side top>
          <q-item-label caption style="color:white;font-size:16px"><b>5 PM</b></q-item-label>
          <q-icon name="alarm" color="secondary" />
        </q-item-section>
      </q-item>

      <q-item>
        <q-item-section>
          <q-item-label caption lines="2" style="color:white;font-size:16px">
           <b>Radiology Clinic
(4D Ultra sound services)
, Annex(Satellite town Branch)</b></q-item-label>
        </q-item-section>

        <q-item-section side top>
          <q-item-label caption style="color:white;font-size:16px"><b>9 AM</b></q-item-label>
          <q-icon name="alarm" color="secondary" />
        </q-item-section>
      </q-item>

      <q-item>
        <q-item-section>
          <q-item-label style="color:#F5FD0D;">Wednesdays</q-item-label>
          <q-item-label caption lines="2" style="color:white;font-size:16px">
            <b>Urologist Clinic
, Annex(Satellite town Branch)</b></q-item-label>
        </q-item-section>

        <q-item-section side top>
          <q-item-label caption style="color:white;font-size:16px"><b>12 PM</b></q-item-label>
          <q-icon name="alarm" color="secondary" />
        </q-item-section>
      </q-item>

            <q-item>
        <q-item-section>
          <q-item-label caption lines="2" style="color:white;font-size:16px">
            <b>O AND G CLINIC (Obstetrician and Gynaecologist)
, Main Branch, Marian</b></q-item-label>
        </q-item-section>

        <q-item-section side top>
          <q-item-label caption style="color:white;font-size:16px"><b>2 PM</b></q-item-label>
          <q-icon name="alarm" color="secondary" />
        </q-item-section>
      </q-item>

            <q-item>
        <q-item-section>
          <q-item-label caption lines="2" style="color:white;font-size:16px">
            <b>O AND G CLINIC (Obstetrician and Gynaecologist)
, Annex(Satellite town Branch)</b></q-item-label>
        </q-item-section>

        <q-item-section side top>
          <q-item-label caption style="color:white;font-size:16px"><b>2 PM</b></q-item-label>
          <q-icon name="alarm" color="secondary" />
        </q-item-section>
      </q-item>

            <q-item>
        <q-item-section>
          <q-item-label caption lines="2" style="color:white;font-size:16px">
           <b>General Surgeon Clinic
, Annex(Satellite town Branch)</b></q-item-label>
        </q-item-section>

        <q-item-section side top>
          <q-item-label caption style="color:white;font-size:16px"><b>5 PM</b></q-item-label>
          <q-icon name="alarm" color="secondary" />
        </q-item-section>
      </q-item>

      <q-item>
        <q-item-section>
          <q-item-label caption lines="2" style="color:white;font-size:16px">
          <b>ENT [Otolaryngology] Clinic
, Main Branch, Marian</b></q-item-label>
        </q-item-section>

        <q-item-section side top>
          <q-item-label caption style="color:white;font-size:16px"><b>5 PM</b></q-item-label>
          <q-icon name="alarm" color="secondary" />
        </q-item-section>
      </q-item>

      <q-item>
        <q-item-section>
          <q-item-label caption lines="2" style="color:white;font-size:16px">
          <b>Ophthalmologist and Optometrists Clinic
, Annex(Satellite town Branch)</b></q-item-label>
        </q-item-section>

        <q-item-section side top>
          <q-item-label caption style="color:white;font-size:16px"><b>5 PM</b></q-item-label>
          <q-icon name="alarm" color="secondary" />
        </q-item-section>
      </q-item>

            <q-item>
        <q-item-section>
          <q-item-label caption lines="2" style="color:white;font-size:16px">
          <b>Radiology Clinic
(4D Ultra sound services)
, Main Branch, Marian</b></q-item-label>
        </q-item-section>

        <q-item-section side top>
          <q-item-label caption style="color:white;font-size:16px"><b>9 AM</b></q-item-label>
          <q-icon name="alarm" color="secondary" />
        </q-item-section>
      </q-item>

      <q-item>
        <q-item-section>
          <q-item-label style="color:#F5FD0D;">Thursday</q-item-label>
          <q-item-label caption lines="2" style="color:white;font-size:16px">
            <b>Ophthalmologist and Optometrists Clinic
, Annex(Satellite town Branch)</b></q-item-label>
        </q-item-section>

        <q-item-section side top>
          <q-item-label caption style="color:white;font-size:16px"><b>5 PM</b></q-item-label>
          <q-icon name="alarm" color="secondary" />
        </q-item-section>
      </q-item>

            <q-item>
        <q-item-section>
          <q-item-label caption lines="2" style="color:white;font-size:16px">
           <b>Radiology Clinic
(4D Ultra sound services)
, Annex(Satellite town Branch)</b></q-item-label>
        </q-item-section>

        <q-item-section side top>
          <q-item-label caption style="color:white;font-size:16px"><b>9 AM</b></q-item-label>
          <q-icon name="alarm" color="secondary" />
        </q-item-section>
      </q-item>

      <q-item>
        <q-item-section>
          <q-item-label style="color:#F5FD0D;">Fridays</q-item-label>
          <q-item-label caption lines="2" style="color:white;font-size:16px">
            <b>Radiology Clinic
(4D Ultra sound services)
, Main Branch, Marian</b></q-item-label>
        </q-item-section>

        <q-item-section side top>
          <q-item-label caption style="color:white;font-size:16px"><b>9 AM</b></q-item-label>
          <q-icon name="alarm" color="secondary" />
        </q-item-section>
      </q-item>

      <q-item>
        <q-item-section>
          <q-item-label style="color:#F5FD0D;">Saturdays</q-item-label>
          <q-item-label caption lines="2" style="color:white;font-size:16px">
         <b>O AND G CLINIC (Obstetrician and Gynaecologist)
, Annex(Satellite town Branch)</b></q-item-label>
        </q-item-section>

        <q-item-section side top>
          <q-item-label caption style="color:white;font-size:16px"><b>11 AM</b></q-item-label>
          <q-icon name="alarm" color="secondary" />
        </q-item-section>
      </q-item>

      <q-item>
        <q-item-section>
          <q-item-label caption lines="2" style="color:white;font-size:16px">
         <b>Pediatrics Clinic
, Main Branch, Marian</b></q-item-label>
        </q-item-section>

        <q-item-section side top>
          <q-item-label caption style="color:white;font-size:16px"><b>4 PM</b></q-item-label>
          <q-icon name="alarm" color="secondary" />
        </q-item-section>
      </q-item>
            <q-item>
        <q-item-section>
          <q-item-label caption lines="2" style="color:white;font-size:16px">
         <b>Cardiologist Clinic
, Main Branch, Marian</b></q-item-label>
        </q-item-section>

        <q-item-section side top>
          <q-item-label caption style="color:white;font-size:16px"><b>5 PM</b></q-item-label>
          <q-icon name="alarm" color="secondary" />
        </q-item-section>
      </q-item>
            <q-item>
        <q-item-section>
          <q-item-label caption lines="2" style="color:white;font-size:16px">
        <b>Physician Clinic
, Main Branch, Marian</b></q-item-label>
        </q-item-section>

        <q-item-section side top>
          <q-item-label caption style="color:white;font-size:16px"><b>5 PM</b></q-item-label>
          <q-icon name="alarm" color="secondary" />
        </q-item-section>
      </q-item>
            <q-item>
        <q-item-section>
          <q-item-label caption lines="2" style="color:white;font-size:16px">
        <b>O AND G CLINIC (Obstetrician and Gynaecologist)
, Main Branch, Marian</b></q-item-label>
        </q-item-section>

        <q-item-section side top>
          <q-item-label caption style="color:white;font-size:16px"><b>9 AM</b></q-item-label>
          <q-icon name="alarm" color="secondary" />
        </q-item-section>
      </q-item>

            <q-item>
        <q-item-section>
          <q-item-label style="color:#F5FD0D;">Saturday and Sunday</q-item-label>
          <q-item-label caption lines="2" style="color:white;font-size:16px">
         <b>Radiology Clinic
(Ultrasound Sound Services)
, Annex(Satellite town Branch)</b></q-item-label>
        </q-item-section>

        <q-item-section side top>
          <q-item-label caption style="color:white;font-size:16px"><b>24/7</b></q-item-label>
          <q-icon name="alarm" color="secondary" />
        </q-item-section>
      </q-item>

    <q-item>
        <q-item-section>
          <q-item-label caption lines="2" style="color:white;font-size:16px">
        <b>Radiology Clinic
(X-ray Services)
, Annex(Satellite town Branch)</b></q-item-label>
        </q-item-section>

        <q-item-section side top>
          <q-item-label caption style="color:white;font-size:16px"><b>24/7</b></q-item-label>
          <q-icon name="alarm" color="secondary" />
        </q-item-section>
      </q-item>

          <q-item>
        <q-item-section>
          <q-item-label caption lines="2" style="color:white;font-size:16px">
       <b>Radiology Clinic
(ECG and Echocardiography)
, Annex(Satellite town Branch)</b></q-item-label>
        </q-item-section>

        <q-item-section side top>
          <q-item-label caption style="color:white;font-size:16px"><b>24/7</b></q-item-label>
          <q-icon name="alarm" color="secondary" />
        </q-item-section>
      </q-item>
      <!-- <q-separator spaced inset /> -->

    </q-list>
  </div>

        </q-card-section>
    </q-dialog>

  <!-- dialog section sum of specialities -->
    <q-dialog v-model="number" id="bgss">
        <q-card-section class="row"  style="">
          <div class="text-h6" style="color:white;">Arubah Clinics</div>
          <q-space/>
          <q-btn
          style="color:white"
          v-close-popup
          icon="close"
          />
    <q-list bordered separator style="width:100%; margin-top:30px; color:white">
      <q-item clickable v-ripple @click="alert1=true">
        <q-item-section>Burns And Plastics</q-item-section>
      </q-item>

      <q-item clickable v-ripple @click="alert2=true">
        <q-item-section>
          <q-item-label>Dental Clinic</q-item-label>
          <!-- <q-item-label caption>Caption</q-item-label> -->
        </q-item-section>
      </q-item>

      <q-item clickable v-ripple @click="alert3=true">
        <q-item-section>
          <!-- <q-item-label overline>OVERLINE</q-item-label> -->
          <q-item-label>General Surgeon Clinic</q-item-label>
        </q-item-section>
      </q-item>
      <q-item clickable v-ripple @click="alert4=true">
        <q-item-section>Nephrologist Clinic</q-item-section>
      </q-item>

      <q-item clickable v-ripple @click="alert5=true">
        <q-item-section>
          <q-item-label>O AND G CLINIC</q-item-label>
          <q-item-label caption style="color:white">(Obstetrician and Gynaecologist)</q-item-label>
        </q-item-section>
      </q-item>

      <q-item clickable v-ripple @click="alert6=true">
        <q-item-section>
          <!-- <q-item-label overline>OVERLINE</q-item-label> -->
          <q-item-label>Pediatrics Clinic</q-item-label>
        </q-item-section>
      </q-item>
            <q-item clickable v-ripple @click="alert7=true">
        <q-item-section>Physiotherapy [physical therapy] Clinic</q-item-section>
      </q-item>

      <q-item clickable v-ripple @click="alert8=true">
        <q-item-section>
          <q-item-label>Cardiologist Clinic</q-item-label>
          <!-- <q-item-label caption>Caption</q-item-label> -->
        </q-item-section>
      </q-item>

      <q-item clickable v-ripple @click="alert9=true">
        <q-item-section>
          <!-- <q-item-label overline>OVERLINE</q-item-label> -->
          <q-item-label>ENT [Otolaryngology] Clinic</q-item-label>
        </q-item-section>
      </q-item>
            <q-item clickable v-ripple @click="alert10=true">
        <q-item-section>Heamaologist</q-item-section>
      </q-item>

      <q-item clickable v-ripple @click="alert11=true">
        <q-item-section>
          <q-item-label>Neurologist Clinic</q-item-label>
          <!-- <q-item-label caption>Caption</q-item-label> -->
        </q-item-section>
      </q-item>

      <q-item clickable v-ripple @click="alert12=true">
        <q-item-section>
          <!-- <q-item-label overline>OVERLINE</q-item-label> -->
          <q-item-label>Ophthalmologist And Optometrists Clinic</q-item-label>
        </q-item-section>
      </q-item>
            <q-item clickable v-ripple @click="alert13=true">
        <q-item-section>Orthopedic Clinic</q-item-section>
      </q-item>

      <q-item clickable v-ripple @click="alert14=true">
        <q-item-section>
          <q-item-label>Physician Clinic</q-item-label>
          <!-- <q-item-label caption>Caption</q-item-label> -->
        </q-item-section>
      </q-item>

      <q-item clickable v-ripple @click="alert15=true">
        <q-item-section>
          <!-- <q-item-label overline>OVERLINE</q-item-label> -->
          <q-item-label>Radiology Clinic</q-item-label>
        </q-item-section>
      </q-item>
            <q-item clickable v-ripple @click="alert16=true">
        <q-item-section>Urologist Clinic</q-item-section>
      </q-item>

    </q-list>
        </q-card-section>

    </q-dialog>

    <!-- <div class="flex flex-center">
    <img style="width:100%; margin-top:;"
      alt="Quasar logo"
      src="~assets/post12.jpg"
    >
</div> -->

<!-- more post -->

  <q-dialog v-model="contact" id="bgf">
        <q-card-section class="row">
          <div class="text-h6 q-pa-md" style="color:white">Contact Us</div>
          <q-space/>
          <q-btn style="color:white"
          v-close-popup
          icon="close"
          />
        </q-card-section>
    <q-list bordered>
      <q-item clickable v-ripple @click="map=true">
        <q-item-section avatar>
          <q-icon color="white" name="map" />
        </q-item-section>

        <q-item-section style="color:white"><b>23 Nsefik Eyo Close, Off Fiesta <br>
Fries, Ndidem Usang Iso Rd. <br>Calabar.</b></q-item-section>
      </q-item>
      <q-item clickable v-ripple>
        <q-item-section avatar>
          <q-icon color="white" name="phone" />
        </q-item-section>

        <q-item-section><a style="text-decoration:none; color:white;" href="tel:+234 811 333 3822"><b>+234 811 333 3822</b></a>
        <br><a style="text-decoration:none; color:white;" href="tel:+234 811 733 3332"><b>+234 811 733 3332</b></a></q-item-section>
      </q-item>
      <q-item clickable v-ripple>
        <q-item-section avatar>
          <q-icon color="white" name="alarm" />
        </q-item-section>

        <q-item-section style="color:white">
<b>Mon - Sun  24Hrs</b></q-item-section>
      </q-item>
         <q-item clickable v-ripple>
        <q-item-section avatar>
          <q-icon color="white" name="mail" />
        </q-item-section>

        <q-item-section>
          <a style="color:blue; text-decoration:none" href="mailto:info@arubahspecialisthospital.com">
            <b>info@arubahspecialisthospital.com</b></a>
</q-item-section>
      </q-item>
       <q-item clickable v-ripple>
        <q-item-section avatar>
          <q-icon color="white" name="forum" />
        </q-item-section>

        <q-item-section>
          <a style="color:blue; text-decoration:none" href="https://www.facebook.com/ashcalabar">
            <b>Facebook</b></a>
</q-item-section>
      </q-item>
       <q-item clickable v-ripple>
        <q-item-section avatar>
          <q-icon color="white" name="chat" />
        </q-item-section>

        <q-item-section>
          <a style="color:blue; text-decoration:none" href="https://instagram.com/ashcalabar">
            <b>Instagram</b></a>
</q-item-section>
      </q-item>

    </q-list>

    </q-dialog>

    <q-dialog v-model="map">
      <q-card>

        <q-card-actions align="right">
          <q-btn flat label="close" color="primary" v-close-popup />
        </q-card-actions>
        <iframe src="https://www.google.com/maps/embed?pb=!1m18!1m12!1m3!1d3974.6715757342677!2d8.343024214090573!3d4.994111240435687!2m3!1f0!2f0!3f0!3m2!1i1024!2i768!4f13.1!3m3!1m2!1s0x106787b0cf55fa75%3A0x210d8162a25422cf!2sNdidem%20Usang%20Iso%20Rd%2C%20Calabar!5e0!3m2!1sen!2sng!4v1595187231549!5m2!1sen!2sng" width="600" height="450" frameborder="0" style="border:0;" allowfullscreen="" aria-hidden="false" tabindex="0"></iframe>
      </q-card>
    </q-dialog>

    <q-dialog v-model="alert1">
      <q-card id="dialo">
        <q-card-section>
          <div class="text-h6">Clinic Time</div>
        </q-card-section>

        <q-card-section class="q-pt-none">
          <span style="font-size:17px">On appointment basis</span>
        </q-card-section>

        <q-card-actions align="right">
          <q-btn flat label="OK" color="primary" v-close-popup />
        </q-card-actions>
      </q-card>
    </q-dialog>

    <q-dialog v-model="alert2">
      <q-card id="dialo">
        <q-card-section>
          <div class="text-h6">Clinic Time</div>
        </q-card-section>

        <q-card-section class="q-pt-none">
           <span style="font-size:17px">Monday to Sunday @ satellite Town Branch, no time</span>
        </q-card-section>

        <q-card-actions align="right">
          <q-btn flat label="OK" color="primary" v-close-popup />
        </q-card-actions>
      </q-card>
    </q-dialog>

    <q-dialog v-model="alert3">
      <q-card id="dialo">
        <q-card-section>
          <div class="text-h6">Clinic Time</div>
        </q-card-section>
        <q-card-section class="q-pt-none">
              <span style="font-size:17px">Wednesdays : 5pm Main Branch or satellite town Branch</span>
        </q-card-section>

        <q-card-actions align="right">
          <q-btn flat label="OK" color="primary" v-close-popup />
        </q-card-actions>
      </q-card>
    </q-dialog>

    <q-dialog v-model="alert4">
      <q-card id="dialo">
        <q-card-section>
          <div class="text-h6">Clinic Time</div>
        </q-card-section>
        <q-card-section class="q-pt-none">
          <span style="font-size:17px">On appointment basis</span>
        </q-card-section>

        <q-card-actions align="right">
          <q-btn flat label="OK" color="primary" v-close-popup />
        </q-card-actions>
      </q-card>
    </q-dialog>

    <q-dialog v-model="alert5">
      <q-card id="dialo">
        <q-card-section>
          <div class="text-h6">Clinic Time</div>
        </q-card-section>

        <q-card-section class="q-pt-none">
            <span style="font-size:17px">Wednesdays : 2pm Main Branch</span><br>

            <span style="font-size:17px">Saturdays : 9am Main Branch</span><br>
            <span style="font-size:17px">Wednesdays : 11am Satellite Town Branch</span>
        </q-card-section>

        <q-card-actions align="right">
          <q-btn flat label="OK" color="primary" v-close-popup />
        </q-card-actions>
      </q-card>
    </q-dialog>

    <q-dialog v-model="alert6">
      <q-card id="dialo">
        <q-card-section>
          <div class="text-h6">Clinic Time</div>
        </q-card-section>

        <q-card-section class="q-pt-none">
          <span style="font-size:17px">Tuesdays : 4pm Main Branch or satellite town Branch</span><br>
            <span style="font-size:17px">Saturdays : 4pm Main Branch or satellite town Branch</span>
        </q-card-section>

        <q-card-actions align="right">
          <q-btn flat label="OK" color="primary" v-close-popup />
        </q-card-actions>
      </q-card>
    </q-dialog>

    <q-dialog v-model="alert7">
      <q-card id="dialo">
        <q-card-section>
          <div class="text-h6">Clinic Time</div>
        </q-card-section>

        <q-card-section class="q-pt-none">
          <span style="font-size:17px">On appointment basis</span>
        </q-card-section>

        <q-card-actions align="right">
          <q-btn flat label="OK" color="primary" v-close-popup />
        </q-card-actions>
      </q-card>
    </q-dialog>

    <q-dialog v-model="alert8">
      <q-card id="dialo">
        <q-card-section>
          <div class="text-h6">Clinic Time</div>
        </q-card-section>

        <q-card-section class="q-pt-none">
          <span style="font-size:17px">Tuesdays : 5pm Main Branch or satellite town Branch</span><br>
            <span style="font-size:17px">Saturdays : 5pm Main Branch or satellite town Branch</span>
        </q-card-section>

        <q-card-actions align="right">
          <q-btn flat label="OK" color="primary" v-close-popup />
        </q-card-actions>
      </q-card>
    </q-dialog>

    <q-dialog v-model="alert9">
      <q-card id="dialo">
        <q-card-section>
          <div class="text-h6">Clinic Time</div>
        </q-card-section>

        <q-card-section class="q-pt-none">
          <span style="font-size:17px">Wednesdays : 5pm Main Branch or satellite town Branch</span><br>
        </q-card-section>

        <q-card-actions align="right">
          <q-btn flat label="OK" color="primary" v-close-popup />
        </q-card-actions>
      </q-card>
    </q-dialog>

    <q-dialog v-model="alert10">
      <q-card id="dialo">
        <q-card-section>
          <div class="text-h6">Clinic Time</div>
        </q-card-section>

        <q-card-section class="q-pt-none">
            <span style="font-size:17px">On appointment basis</span>
        </q-card-section>

        <q-card-actions align="right">
          <q-btn flat label="OK" color="primary" v-close-popup />
        </q-card-actions>
      </q-card>
    </q-dialog>

    <q-dialog v-model="alert11">
      <q-card id="dialo">
        <q-card-section>
          <div class="text-h6">Clinic Time</div>
        </q-card-section>

        <q-card-section class="q-pt-none">
                    <span style="font-size:17px">On appointment basis</span>
        </q-card-section>

        <q-card-actions align="right">
          <q-btn flat label="OK" color="primary" v-close-popup />
        </q-card-actions>
      </q-card>
    </q-dialog>

    <q-dialog v-model="alert12">
      <q-card id="dialo">
        <q-card-section>
          <div class="text-h6">Clinic Time</div>
        </q-card-section>

        <q-card-section class="q-pt-none">
            <span style="font-size:17px">Tuesdays : 2pm Main Branch or satellite town Branch</span><br>
            <span style="font-size:17px">Wednesdays : 5pm Main Branch or satellite town Branch</span><br>
            <span style="font-size:17px">Thursdays : 5pm Main Branch or satellite town Branch</span><br>
            <span style="font-size:17px">Saturdays : 10am at satellite Town Branch</span>
        </q-card-section>

        <q-card-actions align="right">
          <q-btn flat label="OK" color="primary" v-close-popup />
        </q-card-actions>
      </q-card>
    </q-dialog>

    <q-dialog v-model="alert13">
      <q-card id="dialo">
        <q-card-section>
          <div class="text-h6">Clinic Time</div>
        </q-card-section>

        <q-card-section class="q-pt-none">
          <span style="font-size:17px">On appointment basis</span>
        </q-card-section>

        <q-card-actions align="right">
          <q-btn flat label="OK" color="primary" v-close-popup />
        </q-card-actions>
      </q-card>
    </q-dialog>

    <q-dialog v-model="alert14">
      <q-card id="dialo">
        <q-card-section>
          <div class="text-h6">Clinic Time</div>
        </q-card-section>

        <q-card-section class="q-pt-none">
           <span style="font-size:17px">Tuesdays : 5pm Main Branch or satellite town Branch</span><br>
            <span style="font-size:17px">Saturdays : 5pm Main Branch or satellite town Branch</span>
        </q-card-section>

        <q-card-actions align="right">
          <q-btn flat label="OK" color="primary" v-close-popup />
        </q-card-actions>
      </q-card>
    </q-dialog>

    <q-dialog v-model="alert15">
      <q-card id="dialo" class="q-pt-lg">
        <q-card-section>
          <div class="text-h6">Clinic Time</div>
        </q-card-section>

        <q-card-section class="q-pt-none">
            <span style="font-size:17px;">Mondays : 9am Main Branch or satellite town Branch</span><br>
            <span style="font-size:17px">Tuesdays : 9am Main Branch or satellite town Branch</span><br>
            <span style="font-size:17px">Wednesdays : 9am Main Branch or satellite town Branch</span><br>
            <span style="font-size:17px">Thursdays : 9am Main Branch or satellite town Branch</span><br>
            <span style="font-size:17px">Fridays : 9am Main Branch or satellite town Branch</span><br>
            <span style="font-size:17px">Saturdays & Sundays : 24/7 Main Branch or satellite town Branch</span>
        </q-card-section>

        <q-card-actions align="right">
          <q-btn flat label="OK" color="primary" v-close-popup />
        </q-card-actions>
      </q-card>
    </q-dialog>

    <q-dialog v-model="alert16">
      <q-card id="dialo">
        <q-card-section>
          <div class="text-h6">Clinic Time</div>
        </q-card-section>

        <q-card-section class="q-pt-none">
           <span style="font-size:17px">Wednesdays : 12pm Main Branch or satellite town Branch</span><br>
        </q-card-section>

        <q-card-actions align="right">
          <q-btn flat label="OK" color="primary" v-close-popup />
        </q-card-actions>
      </q-card>
    </q-dialog>

  </q-page>


</template>

<script>


export default {
  components: {

  },
  time: 'PageIndex',
data () {
  return {
    alert1: false,
    alert2: false,
    alert3: false,
    alert4: false,
    alert5: false,
    alert6: false,
    alert7: false,
    alert8: false,
    alert9: false,
    alert10: false,
    alert11: false,
    alert12: false,
    alert13: false,
    alert14: false,
    alert15: false,
    alert16: false,
    map: false,
    contact: false,
    slide: 1,
    faq : false,
    time : false,
    post : false,
    post6 : false,
    post4 : false,
    post3 : false,
    post2 : false,
    post7 : false,
    post8 : false,
    post9 : false,
    post10 : false,
    number : false,
    fullscreen: false,

      pagination: {
        rowsPerPage: 0
      },
  }
},

methods:{
  toUsers(){
    this.$router.push('/users')
  },
  toDocs(){
    this.$router.push('/doc')
  }
},
}
</script>
<style>
  #bg{
    background-image:url('~assets/v_slide/landing.jpg');
    background-repeat: no-repeat;
    background-size: cover;
    /* background-attachment: fixed; */
}
  #bgs{
    background-image:url('~assets/v_slide/viewer.jpg');
    background-repeat: no-repeat;
    background-size: cover;
}
  #bgss{
    background-image:url('~assets/v_slide/oneee.jpg');
    background-repeat: no-repeat;
    background-size: cover;
}
  #bgt{
    background-image:url('~assets/v_slide/twooo.jpg');
    background-repeat: no-repeat;
    background-size: cover;
}
  #bgf{
    background-image:url('~assets/v_slide/fourrr.jpg');
    background-repeat: no-repeat;
    background-size: cover;
}
  #dialo{
    border-radius:20%
    /* animation-name:dialog;
    animation-duration:5s; */
  }
  /* @keyframes dialog{
    0% { border-radius:5%}
    25% { border-radius:20%}
    50% { border-radius:30%}
    75% { border-radius:40%}
    100% { border-radius:50%}
  } */

</style>
