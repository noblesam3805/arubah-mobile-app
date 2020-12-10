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
  <q-btn icon="send"
   @click="s_all_p=true"
   style="width:100px" label="Send Name" stack glossy color="green-8" class="q-ma-md"/>
  <q-btn icon="check_circle"
  @click="see_a=true"
   style="width:150px" label="Appointments" stack glossy color="red-8" class="q-ma-md"/>
</div>
<!-- <div class="text-center">
  <q-btn icon="people" style="width:100px" label="Admitted Patients" stack glossy color="red-8" class="q-ma-md"/>
  <q-btn icon="cast" style="width:150px" label="Broadcast" stack glossy color="green-8" class="q-ma-md"/>
</div> -->
  <div class="flex flex-center">
    <img style="width:100%; margin-top:;"
      alt="Quasar logo"
      src="~assets/post1.jpg">
    </div>
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

    <!-- see all sent patient name dialogue -->
    <q-dialog v-model="s_all_p">
      <q-card>
        <q-card-section class="row"><q-btn
            style="margin-left:83%;"
          v-close-popup
          icon="close"
          class=""
          />
          <div class="text-h6">Patients Who Sent Their Names

            <p class="caption" style="font-size:15px; color:green; margin-left:0px">
             send patient name to nurse </p></div>
          <!-- <q-space/> -->

        </q-card-section>
        <q-card-section>
          <q-banner style="margin:15% 0 0 23%; width:50%"
            v-if="msg"
            @click="msg = ''"
            class="q-mb-md bg-warning text-center fixed-top"
            >
            {{msg}}
            </q-banner>

        </q-card-section>
  <table style="margin-right:50px;" v-if="Object.keys(sPatients).length">
  <tr>
    <th>Firstname</th>
    <th>Lastname</th>
    <th>Sex</th>
    <th>Reg Date</th>
    <th>Option</th>
  </tr>
  <tr v-for="sPatient in sPatients" :key="sPatient.patient_id">
    <td>{{sPatient.first_name}}</td>
    <td>{{sPatient.last_name}}</td>
    <td>{{sPatient.sex}}</td>
    <td>{{sPatient.reg_date}} </td>
    <td><q-btn label="send"  @click="uSPatients(sPatient)"/></td>
  </tr>

</table>
      </q-card>

    </q-dialog>

    <q-dialog v-model="see_a">
      <q-card>
        <q-card-section class="row">
          <div class="text-h6 p-md-a">All Appointments</div>
          <q-space/>
          <q-btn
          v-close-popup
          icon="close"
          class="fixed"
          style="margin-left:70%"
          />
        </q-card-section>
          <q-banner style="margin:15% 0 0 23%; width:50%"
            v-if="msg"
            @click="msg = ''"
            class="q-mb-md bg-warning text-center fixed-top"
            >
            {{msg}}
            </q-banner>

  <table style="margin-right:50px;" v-if="Object.keys(rAppointments).length">
  <tr>
    <th>Patient ID</th>
    <th>Reason For Appointment</th>
    <th>Status</th>
    <th>Time</th>
    <th>Date</th>
    <th>Clinic</th>
    <th>Option</th>

  </tr>
  <tr v-for="rAppointment in rAppointments" :key="rAppointment.id">
    <td>{{rAppointment.patient_id}} </td>
    <td>{{rAppointment.complain}}</td>
    <td>{{rAppointment.status}}</td>
    <td>{{rAppointment.realtime}}</td>
    <td>{{rAppointment.timestamp}}</td>
    <td>{{rAppointment.clinic}}</td>
    <td><q-btn label="approve"  @click="uRAppointments(rAppointment)"/><br><br>
        <q-btn label="disapprove"  @click="bUComment(rAppointment)"/>
    </td>

  </tr>

</table>
      </q-card>

    </q-dialog>

  <q-dialog v-model="comment">
      <q-card>
        <q-card-section class="row"><q-btn
          v-close-popup
          icon="close"
          style="margin-left:230px"
          />
          <div class="text-h6 p-md-a">Drop A Reason For Disapproval</div>
          <q-space/>

        </q-card-section>
          <q-banner style="margin:15% 0 0 23%; width:50%"
            v-if="msg"
            @click="msg = ''"
            class="q-mb-md bg-warning text-center fixed-top"
            >
            {{msg}}
            </q-banner>
            <q-input autofocus filled v-model="commen" label="comment" class="q-mb-md q-ma-md" />
            <q-btn label="comment" @click="dRAppointments"  class="q-mb-md q-ma-md bg-green text-center"/>
      </q-card>

    </q-dialog>

  </q-pull-to-refresh>



</template>

<script>
export default {
  name: 'PageIndex',
data(){
  return {
    slide: 1,
    alert: true,
    s_all_p : false,
    msg : '',
    see_a : false,
    comment : false,
    commen : '',
    id : '',
    doctor_id : '',
    patient_id : '',
    complain : '',
    sPatients:[{
      }],
  rAppointments:[{
      }],
  }
},
mounted(){
  this.aSentPatients();
  this.aAppointments();
  // this.aAPatients();
  // this.bedSpace();
},
methods:{
  refresher (done) {
      setTimeout(() => {
        done()
        window.location.reload()
      }, 1000)
},
      bUComment(rAppointment){
        this.comment = true
        this.id = rAppointment.appointment_id
        this.doctor_id = rAppointment.doctor_id
        this.patient_id = rAppointment.patient_id
        this.complain = rAppointment.complain
      },
      dRAppointments(id){
         this.msg = ''
         console.log(this.id)

        fetch("https://app.arubahspecialisthospital.com/index.php?mobileloginservice/updateBookedAppointment/"+this.id, {
         method: "POST",
         body: JSON.stringify({
           doctor_id: this.doctor_id,
           patient_id:this.patient_id,
           complain:this.complain,
           status: this.commen,
         }),
         headers: {
           "Content-type": "application/json"
            }
        })
        .then(res => res.text())
        .then(res => {
          console.log(res)
          if(res == "success"){
          this.msg = 'Appointment Disapproved Successfully'
          this.aAppointments();
          }
        })

      },
      uRAppointments(rAppointment){
        this.msg = ''
         console.log(rAppointment.appointment_id)
        fetch("https://app.arubahspecialisthospital.com/index.php?mobileloginservice/updateBookedAppointment/"+rAppointment.appointment_id, {
         method: "POST",
         body: JSON.stringify({
           doctor_id: rAppointment.doctor_id,
           patient_id:rAppointment.patient_id,
           complain:rAppointment.complain,
           status: 'approved',
         }),
         headers: {
           "Content-type": "application/json"
            }
        })
        .then(res => res.text())
        .then(res => {
          console.log(res)
          if(res == "success"){
          this.msg = 'Appointment Approved Successfully'
          this.aAppointments();
          }
        })

      },
      aAppointments(){
        // if(this.$route.path == '/patient'){
        fetch("https://app.arubahspecialisthospital.com/index.php?mobileloginservice/getAllAppointment")
        .then(res => res.json())
        .then(res => {
          this.rAppointments = res.Records
          console.log(res)
        })

      },
      aSentPatients(){
        fetch("https://app.arubahspecialisthospital.com/index.php?mobileloginservice/patientsWhoSentName")
        .then(res => res.json())
        .then(res => {
          this.sPatients = res.patientsAttendedToRecords
          console.log(res)
        })
      },
      uSPatients(sPatient){
        fetch("https://app.arubahspecialisthospital.com/index.php?mobileloginservice/updatePatient/"+sPatient.patient_id, {
         method: "POST",
         body: JSON.stringify({
           to_admin: 2
         }),
         headers: {
           "Content-type": "application/json"
            }
        })
        .then(res => res.text())
        .then(res => {
          this.msg = "Name Sent Successfully To Nurse's Account"
          this.aSentPatients();
          console.log(res)
        })
      },
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
  table, td, th {
  border: 1px solid #ddd;
  text-align: left;
}

table {
  border-collapse: collapse;
  width: 100%;
}

th, td {
  padding: 15px;
}
</style>
