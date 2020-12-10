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


<div class="text-center">
  <q-btn icon="people"
   @click="pAttendedTo = true"
   style="width:100px" label="Patients attended to" stack glossy color="green-8" class="q-ma-md"/>
  <q-btn icon="people"
  @click="patients = true"
   style="width:150px" label="Patients from admin" stack glossy color="red-8" class="q-ma-md"/>
</div>
  <div class="flex flex-center">
    <img style="width:100%; margin-top:;"
      alt="Quasar logo"
      src="~assets/post1.jpg">
    </div>


<!-- dialog section -->
    <q-dialog v-model="patients">
      <q-card>
        <q-card-section class="row">
          <div class="text-h6 q-mr-md">Patients From Admin
            <p class="caption" style="font-size:15px; color:green; margin-left:10px">
              click to mark done</p></div>
          <q-space/>
          <q-btn
          v-close-popup
          icon="close"

          />
        </q-card-section>
        <q-card-section>
          <q-banner style="margin:15% 0 0 23%; width:50%"
            v-if="msg"
            @click="msg = ''"
            class="q-mb-md bg-warning text-center fixed-top"
            >
            {{msg}}
            </q-banner>
        <q-card-section style="margin-top:-30px;" class="q-pa-md" v-if="Object.keys(rPatients).length">
      <q-list  style="background-color:#fff; width:100%" bordered  v-for="rPatient in rPatients" :key="rPatient.patient_id">
       <q-item
      @click="uRPatients(rPatient)"
      clickable
      >

        <q-item-section>
          <q-item-label>
           {{rPatient.first_name}}  {{rPatient.last_name}}
          </q-item-label>
        </q-item-section>

<div class="row">
  <div class="column">


        <q-item-section class="q-ml-md">
          <q-item-label caption >
           {{rPatient.sex}}
          </q-item-label>

          <q-item-label v-if="rPatient.reg_date" caption class="row justify-end">
            <q-icon name="event" size="14px" class=""/>
          <small> {{rPatient.reg_date}}  </small>

          </q-item-label>
        </q-item-section>
  </div>

</div>
</q-item>
    </q-list>
        </q-card-section>
        </q-card-section>
      </q-card>
    </q-dialog>

<!-- patients attended to -->

<q-dialog v-model="pAttendedTo">
      <q-card>
        <q-card-section class="row">
          <div class="text-h6 q-mr-md">Patients Attended To
            <p class="caption" style="font-size:15px; color:green; margin-left:10px">
             all patients attended to</p></div>
          <q-space/>
          <q-btn
          v-close-popup
          icon="close"

          />
        </q-card-section>
        <q-card-section>
          <q-banner style="margin:15% 0 0 23%; width:50%"
            v-if="msg"
            @click="msg = ''"
            class="q-mb-md bg-warning text-center fixed-top"
            >
            {{msg}}
            </q-banner>
        <q-card-section style="margin-top:-30px;" class="q-pa-md" v-if="Object.keys(PatientsAT).length">
      <q-list  style="background-color:#fff; width:100%" bordered  v-for="PatientAT in PatientsAT" :key="PatientAT.patient_id">
       <q-item
      clickable
      >

        <q-item-section>
          <q-item-label>
           {{PatientAT.first_name}}  {{PatientAT.last_name}}
          </q-item-label>
        </q-item-section>

<div class="row">
  <div class="column">

        <q-item-section class="q-ml-md">
          <q-item-label caption >
           {{PatientAT.sex}}
          </q-item-label>

          <q-item-label v-if="PatientAT.reg_date" caption class="row justify-end">
            <q-icon name="event" size="14px" class=""/>
          <small> {{PatientAT.reg_date}}  </small>

          </q-item-label>
        </q-item-section>
  </div>

</div>
      </q-item>

    </q-list>
        </q-card-section>
        </q-card-section>
      </q-card>

    </q-dialog>
  </q-page>

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
</q-pull-to-refresh>
</template>

<script>
export default {
  name: 'PageIndex',
data(){
  return{
    slide : 1,
    pAttendedTo : false,
    patients : false,
    msg : '',
    alert: true,
    rPatients : [{

    }],
    PatientsAT : [{

    }],
  }
},
mounted(){
  this.aRPatients();
  this.aPatientsAT();
},
methods:{
  refresher (done) {
      setTimeout(() => {
        done()
        window.location.reload()
      }, 1000)
},
  toDocs(){
    this.$router.push('/doc')
  },
  uRPatients(rPatient){
    fetch("https://app.arubahspecialisthospital.com/index.php?mobileloginservice/updatePatient/"+rPatient.patient_id, {
     method: "POST",
     body: JSON.stringify({
       to_admin: 3
     }),
     headers: {
       "Content-type": "application/json"
        }
    })
    .then(res => res.text())
    .then(res => {
      this.msg = res
      this.aRPatients();
      this.aPatientsAT();
      console.log(res)
    })
  },
     aRPatients(){
     fetch("https://app.arubahspecialisthospital.com/index.php?mobileloginservice/patientSentToNurse")
     .then(res => res.json())
     .then(res => {
       this.rPatients = res.sentToNurseRecords
       console.log(res)
     })
  },
  aPatientsAT(){
     fetch("https://app.arubahspecialisthospital.com/index.php?mobileloginservice/patientsAttendedTo")
     .then(res => res.json())
     .then(res => {
       this.PatientsAT = res.patientsAttendedToRecords
       console.log(res)
     })
  },
},
}
</script>
