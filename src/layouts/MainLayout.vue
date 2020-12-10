<template>
  <q-layout view="lHh Lpr lFf">
    <q-dialog v-model="success">
      <q-card>
        <!-- <q-card-section>
          <div class="text-h6">Disclaimer: </div>
        </q-card-section> -->

        <q-card-section class="q-ma-md">
          <h5>You are logged in</h5>
        </q-card-section>

        <q-card-actions align="right">
          <q-btn flat label="OK" color="primary" v-close-popup />
        </q-card-actions>
      </q-card>
    </q-dialog>
    <q-header id=""  color="primary" elevated v-if="this.$route.path !='/' && this.$route.path !='/s_view'"
    style="border:0px solid #37A000;border-radius:0 0 0 0;"
    >
      <q-toolbar>
        <q-btn v-if="this.$route.path == '/viewer'  || this.$route.path == '/home'
        || this.$route.path == '/admin'
        || this.$route.path == '/doctor' || this.$route.path == '/patient'"
          flat
          dense
          round
          icon="menu"
          aria-label="Menu"
          @click="leftDrawerOpen = !leftDrawerOpen"
        />
         <q-btn v-if="this.$route.params.otherUserId || this.$route.path == '/users'
         || this.$route.path == '/doc'"
          v-go-back.single
          flat
          dense
          round
          icon="arrow_back"
          aria-label="Back"

        />

        <q-toolbar-title class="absolute-center">
          {{title}}
        </q-toolbar-title>
          <!-- icon="account_circle" -->
        <q-btn style="padding-left:210px;"
          v-if="userDetails.userId"
          @click="logoutUser"
          class="absolute-right q-pr-sm"
          no-caps
          flat
          dense>
          Logout<br>
          {{ userDetails.name }}
        </q-btn>
         <q-btn style="padding-left:210px;"
          v-if="this.$route.path == '/doctor' || this.$route.path == '/admin'
          || this.$route.path == '/nurse' || this.$route.path == '/patient'"
          @click="logout"
          class="absolute-right q-pr-sm"
          no-caps
          flat
          dense>
          Logout<br>
          {{u_name}}
          <!-- <span v-if="this.$route.path=='/patient' || this.$route.path=='/admin'">{{u_name}}</span> -->
        </q-btn>

      </q-toolbar>
    </q-header>

    <!-- <q-footer v-if="this.$route.path == '/admin'">
        <q-tabs >
          <q-route-tab
          to="/admin" icon="home"/>
          <q-route-tab
          to="" icon="chat"/>

        </q-tabs>
    </q-footer> -->
    <q-footer v-if="this.$route.path == '/c_login'">
        <q-tabs >
          <q-route-tab
          to="/viewer" icon="home"/>
          <q-route-tab
          to="/c_login" icon="perm_identity"/>

        </q-tabs>
    </q-footer>
      <q-footer v-if="this.$route.path == '/login'">
        <q-tabs >
          <q-route-tab
          to="/viewer" icon="home"/>
          <q-route-tab
          to="/login" icon="perm_identity"/>

        </q-tabs>
    </q-footer>
     <q-footer v-if="this.$route.path == '/viewer'">
        <q-tabs >
          <q-route-tab
          to="/login" icon="perm_identity" label=""/>
          <q-route-tab
          to="/viewer" icon="home" label=""/>


        </q-tabs>
    </q-footer>
      <q-footer v-if="this.$route.path == '/viewer' && user_type == 'patient'">
        <q-tabs >
          <q-route-tab
          to="/patient" icon="perm_identity" label=""/>
          <q-route-tab
          to="/viewer" icon="home" label=""/>


        </q-tabs>
    </q-footer>
          <q-footer v-if="this.$route.path == '/viewer' && user_type == 'admin'">
        <q-tabs >
          <q-route-tab
          to="/admin" icon="perm_identity" label=""/>
          <q-route-tab
          to="/viewer" icon="home" label=""/>


        </q-tabs>
    </q-footer>
          <q-footer v-if="this.$route.path == '/viewer' && user_type == 'nurse'">
        <q-tabs >
          <q-route-tab
          to="/nurse" icon="perm_identity" label=""/>
          <q-route-tab
          to="/viewer" icon="home" label=""/>


        </q-tabs>
    </q-footer>
          <q-footer v-if="this.$route.path == '/viewer' && user_type == 'doctor'">
        <q-tabs >
          <q-route-tab
          to="/doctor" icon="perm_identity" label=""/>
          <q-route-tab
          to="/viewer" icon="home" label=""/>


        </q-tabs>
    </q-footer>
     <q-footer v-if="this.$route.path == '/home'">
        <q-tabs >
          <q-route-tab
          to="/doc" icon="chat" label=""/>
          <q-route-tab
          to="/home" icon="home" label=""/>
        </q-tabs>
    </q-footer>
    <q-footer v-if="this.$route.path == '/patient' && user_type == 'patient'">
        <q-tabs >
          <q-route-tab
          to="/patient" icon="perm_identity" label=""/>
          <q-route-tab
          to="/viewer" icon="home" label=""/>


        </q-tabs>
    </q-footer>
    <q-footer v-if="this.$route.path == '/admin' && user_type == 'admin'">
        <q-tabs >
          <q-route-tab
          to="/admin" icon="perm_identity" label=""/>
          <q-route-tab
          to="/viewer" icon="home" label=""/>


        </q-tabs>
    </q-footer>

    <q-drawer
    v-if="this.$route.path == '/viewer'  || this.$route.path =='/home'
    || this.$route.path =='/admin' ||
    !this.$route.params.otherUserId"
      v-model="leftDrawerOpen"
      show-if-above
      bordered
      content-class="bg-white-2"
    >
      <q-list
      id="draw"
      separator v-if="this.$route.path == '/home' || this.$route.path == '/viewer' ">
        <q-item-label
          header
          class="text-green-5"
        >
          Essential Links
        </q-item-label>
        <EssentialLink
          v-for="link in essentialLinks"
          :key="link.title"
          v-bind="link"
        />
      </q-list>

       <!-- links admin -->

    <q-list separator v-if="this.$route.path == '/admin' ">
        <q-item-label
          header
          class="text-grey-8"
        >
          Admin
        </q-item-label>
        <!-- <div style="margin:0% 0 0% 5%; padding:5%"
          @click="see_a=true"
          class="row"
          clickable
          tag="a"
          target="_blank"
          href=""
        >
          <q-item-section
            avatar
          >
            <q-icon name="check_circle" />
          </q-item-section>

          <q-item-section>
            <q-item-label>Appointment</q-item-label>
            <q-item-label caption>
              approve appointment
            </q-item-label>
          </q-item-section>
        </div> -->
          <!-- <div style="margin:0% 0 0% 5%; padding:5%"
          @click="booking=true"
          clickable
          tag="a"
          target="_blank"
          href=""
        > -->
          <!-- <q-item-section
            avatar
          >
            <q-icon name="check_circle" />
          </q-item-section> -->

          <!-- <q-item-section>
            <q-item-label>Book Appointment</q-item-label>
            <q-item-label caption>
              book appointment
            </q-item-label>
          </q-item-section> -->
        <!-- </div> -->
        <!-- <div style="margin:0% 0 0% 5%; padding:5%"
          @click="s_all_p=true"
          class="row"
          clickable
          tag="a"
          target="_blank"
          href=""
        >
          <q-item-section
            avatar
          >
            <q-icon name="send" />
          </q-item-section>

          <q-item-section>
            <q-item-label>Send Name</q-item-label>
            <q-item-label caption>
              send patient name to nurses
            </q-item-label>
          </q-item-section>
        </div> -->

    </q-list>

        <!-- links doctor -->

    <q-list id="draw" v-if="this.$route.path == '/doctor'">
        <q-item-label
          header
          class="text-grey-8"
        >
          Doctor
        </q-item-label>
         <div style="margin:0% 0 0% 5%; padding:5%"
          @click="pInfo=true"
          clickable
          tag="a"
          target="_blank"
          href=""
        >
          <!-- <q-item-section
            avatar
          >
            <q-icon name="check_circle" />
          </q-item-section> -->

          <q-item-section>
            <q-item-label id="lab">Patient Info</q-item-label>
            <q-item-label id="cap" caption>
              document patient info
            </q-item-label>
          </q-item-section>
        </div>
         <div style="margin:0% 0 0% 5%; padding:5%"
          @click="rInvestigation=true"
          clickable
          tag="a"
          target="_blank"
          href=""
        >
          <!-- <q-item-section
            avatar
          >
            <q-icon name="check_circle" />
          </q-item-section> -->

          <q-item-section>
            <q-item-label id="lab">Investigation</q-item-label>
            <q-item-label id="cap" caption>
              request for investigation
            </q-item-label>
          </q-item-section>
        </div>
        <div style="margin:0% 0 0% 5%; padding:5%"
          @click="sPrescription=true"
          clickable
          tag="a"
          target="_blank"
          href=""
        >
          <!-- <q-item-section
            avatar
          >
            <q-icon name="check_circle" />
          </q-item-section> -->

          <q-item-section>
            <q-item-label id="lab">Prescription</q-item-label>
            <q-item-label id="cap" caption>
              send prescription request
            </q-item-label>
          </q-item-section>
        </div>
        <div style="margin:0% 0 0% 5%; padding:5%"
          @click="m_a_patients=true"
          clickable
          tag="a"
          target="_blank"
          href=""
        >
          <!-- <q-item-section
            avatar
          >
            <q-icon name="check_circle" />
          </q-item-section> -->

          <q-item-section>
            <q-item-label id="lab" >Admitted Patients</q-item-label>
            <q-item-label id="cap" caption>
              manage admitted patients
            </q-item-label>
          </q-item-section>
        </div>
         <div style="margin:0% 0 0% 5%; padding:5%"
          @click="s_i_admin=true"
          clickable
          tag="a"
          target="_blank"
          href=""
        >
          <!-- <q-item-section
            avatar
          >
            <q-icon name="check_circle" />
          </q-item-section> -->

          <q-item-section>
            <q-item-label id="lab" >Send Info</q-item-label>
            <q-item-label id="cap" caption>
              send information to CSO officer(admin)
            </q-item-label>
          </q-item-section>
        </div>
    </q-list>

        <!-- links more admin -->

    <q-list id="draw" separator v-if="this.$route.path == '/admin'">

         <div style="margin:0% 0 0% 5%; padding:5%"
          @click="a_a_p=true"
          class="row"
          clickable
          tag="a"
          target="_blank"
          href=""
        >
          <q-item-section
            avatar
          >
            <q-icon name="people" />
          </q-item-section>

          <q-item-section>
            <q-item-label id="lab" >Admitted Patients</q-item-label>
            <q-item-label id="cap" caption>
              see admitted patients & available bed space
            </q-item-label>
          </q-item-section>
        </div>
          <div style="margin:0% 0 0% 5%; padding:5%"
          @click="s_b=true"
          class="row"
          clickable
          tag="a"
          target="_blank"
          href=""
        >
          <q-item-section
            avatar
          >
            <q-icon name="cast" />
          </q-item-section>

          <q-item-section>
            <q-item-label id="lab" >Send Broadcast</q-item-label>
            <q-item-label id="cap" caption>
              send broadcast messages to all patients
            </q-item-label>
          </q-item-section>
        </div>
      <div style="margin:0% 0 0% 5%; padding:5%"
          @click="u_f=true"
          class="row"
          clickable
          tag="a"
          target="_blank"
          href=""
        >
          <q-item-section
            avatar
          >
            <q-icon name="folder" />
          </q-item-section>

          <q-item-section>
            <q-item-label id="lab" >Upload File</q-item-label>
            <q-item-label id="cap" caption>
              upload files to viewers page
            </q-item-label>
          </q-item-section>
        </div>
        <div style="margin:0% 0 0% 5%; padding:5%"
          @click="t_a=true"
          class="row"
          clickable
          tag="a"
          target="_blank"
          href=""
        >
          <q-item-section
            avatar
          >
            <q-icon name="check" />
          </q-item-section>

          <q-item-section>
            <q-item-label id="lab" >Treated Appointments</q-item-label>
            <q-item-label id="cap" caption>
              see all treated appointments
            </q-item-label>
          </q-item-section>
        </div>
        <div style="margin:0% 0 0% 5%; padding:5%"
          @click="p_a=true"
          class="row"
          clickable
          tag="a"
          target="_blank"
          href=""
        >
          <q-item-section
            avatar
          >
            <q-icon name="replay" />
          </q-item-section>

          <q-item-section>
            <q-item-label id="lab" >Pending Appointments</q-item-label>
            <q-item-label id="cap" caption>
              see all pending appointments
            </q-item-label>
          </q-item-section>
        </div>
        <div style="margin:0% 0 0% 5%; padding:5%"
          @click="a_p=true"
          class="row"
          clickable
          tag="a"
          target="_blank"
          href=""
        >
          <q-item-section
            avatar
          >
            <q-icon name="group" />
          </q-item-section>

          <q-item-section>
            <q-item-label id="lab" >Patients</q-item-label>
            <q-item-label id="cap" caption>
              see all patients
            </q-item-label>
          </q-item-section>
        </div>
         <!-- <div style="margin:0% 0 0% 5%; padding:5%"
          @click="respond=true"
          clickable
          tag="a"
          target="_blank"
          href=""
        > -->
          <!-- <q-item-section
            avatar
          >
            <q-icon name="check_circle" />
          </q-item-section> -->

          <!-- <q-item-section>
            <q-item-label>Respond</q-item-label>
            <q-item-label caption>
              respond to request for results & invoices
            </q-item-label>
          </q-item-section>
        </div> -->
    </q-list>

        <!-- links patient -->

    <q-list id="draw" separator v-if="this.$route.path == '/patient' ">
        <q-item-label
          header
          class="text-grey-8"
        >
          Patient
        </q-item-label>
        <div style="margin:0% 0 0% 5%; padding:5%"
          class="row"
          @click="confirm=true"
          clickable
          tag="a"
          target="_blank"
          href=""
        >
          <q-item-section
            avatar
          >
            <q-icon name="send" />
          </q-item-section>

          <q-item-section>
            <q-item-label id="lab" >Send Name</q-item-label>
            <q-item-label id="cap" caption>
              send name to admin
            </q-item-label>
          </q-item-section>
        </div>
    <q-dialog v-model="confirm" persistent>
      <q-card>
        <q-card-section class="row items-center">
          <q-avatar icon="check_circle" color="primary" text-color="white" />
          <span class="q-ml-sm">Proceed to send name.</span>
        </q-card-section>

        <q-card-actions align="right">
          <q-btn flat label="Cancel" color="primary" v-close-popup />
          <q-btn flat label="OK" @click="updatePatient" color="primary" v-close-popup />
        </q-card-actions>
      </q-card>
    </q-dialog>
        <div
        class="row"
        style="margin:0% 0 0% 5%; padding:5%"
          @click="appointment =true"
          clickable
          tag="a"
          target="_blank"
          href=""
        >
          <q-item-section
            avatar
          >
            <q-icon name="book" />
          </q-item-section>

          <q-item-section>
            <q-item-label id="lab" >Appointment</q-item-label>
            <q-item-label id="cap" caption>
              book an appointment
            </q-item-label>
          </q-item-section>
        </div>
        <div style="margin-left:5%; padding:5%"
          @click="result =true"
          class="row"
          clickable
          tag="a"
          target="_blank"
          href=""
        >
          <q-item-section
            avatar
          >
            <q-icon name="check_circle" />
          </q-item-section>

          <q-item-section>
            <q-item-label id="lab" >Status</q-item-label>
            <q-item-label id="cap" caption>
              See appointment status
            </q-item-label>
          </q-item-section>
        </div>
        <div style="margin-left:5%; padding:5%"
          class="row"
          @click="request =true"
          clickable
          tag="a"
          target="_blank"
          href=""
        >
          <q-item-section
            avatar
          >
            <q-icon name="cast" />
          </q-item-section>

          <q-item-section>
            <q-item-label id="lab" >Broadcast</q-item-label>
            <q-item-label id="cap" caption>
              see broadcast messages
            </q-item-label>
          </q-item-section>
        </div>
      <q-dialog v-model="request" persistent>
      <q-card>
        <q-card-section class="row">
          <q-btn
          style="margin-left:230px"
          v-close-popup
          icon="close"
          />
          <div class="text-h6 q-pa-md">Broadcast Messages</div>
          <q-space/>

        </q-card-section>
<q-card-section v-if="Object.keys(bMsgs).length">
<q-list  bordered  v-for="bMsg in bMsgs" :key="bMsg.message_id">
       <q-item class="bg-green">
        <q-item-section>
          <q-item-label style="">
           {{bMsg.message_body}}
          </q-item-label>
        </q-item-section>
<div class="row">
  <div class="column">
        <q-item-section class="q-ml-md">
          <q-item-label caption >
           {{bMsg.sender_id}}
          </q-item-label>

          <q-item-label caption class="row justify-end">
            <q-icon name="event" size="14px" class=""/>
          <small> {{bMsg.message_timestamp}}  </small>

          </q-item-label>
        </q-item-section>
  </div>
  </div>
      </q-item>
    </q-list>
      </q-card-section>
 </q-card>
    </q-dialog>
       <div style="margin:0% 0 0% 5%; padding:5%"
          @click="payment =true"
          class="row"
          clickable
          tag="a"
          target="_blank"
          href=""
        >
          <q-item-section
            avatar
          >
            <q-icon name="money" />
          </q-item-section>

          <q-item-section>
            <q-item-label id="lab" >Payment</q-item-label>
            <q-item-label id="cap" caption>
              make payments for invoices
            </q-item-label>
          </q-item-section>
        </div>

      </q-list>
    </q-drawer>

    <q-page-container>
      <router-view />
    </q-page-container>

    <!-- appointment -->

    <q-dialog v-model="appointment">
      <q-card>
   <form @submit.prevent="bookAppointment">
        <q-card-section class="row">
          <div class="text-h6">Book Appointment</div>
          <q-space/>
          <q-btn
          v-close-popup
          icon="close"

          />
        </q-card-section>
  <q-banner style="margin:0 10% 0 10%;"
    v-if="msg"
    @click="msg = ''"
    class="q-mb-md bg-warning text-center"
    >
    {{msg}}
  </q-banner>
        <q-card-section>
          <div class="q-mb-md">
          <q-select outlined v-model="clinic" :options="options" label="select clinic" />


          </div>
           <div class="q-mb-md">
            <q-input outlined v-if="clinic!='Urologist Clinic'
            && clinic !='General Surgeon Clinic' && clinic !='ENT [Otolaryngology] Clinic'" label="clinic time" v-model="time"
            >
              <template v-slot:append>
                 <q-icon name="close"
                 class="cursor-pointer"
                  >
                </q-icon>

                <q-icon name="access_time" class="cursor-pointer">
                  <q-popup-proxy>
                    <q-time v-model="time"/>
                  </q-popup-proxy>
                </q-icon>
              </template>
            </q-input>
            </div>
          <div class="q-mb-md">
          <q-input
          ref="complain"
          required
          outlined
          v-model="complain"
          label="any special requests"
          >
              <template v-slot:append>
                <q-icon name="close"
                 class="cursor-pointer"

                 >
                </q-icon>
              </template>
          </q-input>

          </div>
          <div  class="q-mb-md">
            <q-input outlined  label="date"
              v-model="date" required>
              <template v-slot:append>
                  <q-icon name="close"
                 class="cursor-pointer"
                 >
                </q-icon>

                <q-icon name="event" class="cursor-pointer">
                  <q-popup-proxy>
                    <q-date v-model="date"/>
                  </q-popup-proxy>
                </q-icon>
              </template>
            </q-input>
          </div>

        </q-card-section>
         <q-card-actions  align="right">
        <q-btn
        type="submit"
          color="primary"
          label="book"
          />
         </q-card-actions>
         </form>
      </q-card>

    </q-dialog>

    <!-- payment -->

    <q-dialog v-model="payment">
      <q-card>


        <q-card-section class="row">
          <div class="text-h6">Make Payment</div>
          <q-space/>
          <q-btn
          v-close-popup
          icon="close"

          />
        </q-card-section>
        <q-card-section>
          <div  class="q-mb-md">
          <q-input
          ref="amount"
          required
          autofocus
          outlined
          type="number"
          label="amount in kobo"
          v-model="amount"
          >
          <template v-slot:append>
                <q-icon name="close"
                 class="cursor-pointer"
                >
            </q-icon>
          </template>
          </q-input>
          </div>
           <div  class="q-mb-md">
          <q-input
          ref="email"
          required

          outlined
          type="email"
          label="email"
          v-model="email"
          >
          <template v-slot:append>
                <q-icon name="close"
                 class="cursor-pointer"
                >
            </q-icon>
          </template>
          </q-input>

          </div>

        </q-card-section>
        <paystack
        :amount="amount"
        :email="email"
        :paystackkey="paystackkey"
        :reference="reference"
        :callback="callback"
        :close="close"
        :embed="false"
    >
         <q-card-actions  align="right">
        <q-btn
        type="submit"
          color="primary"
          label="pay"
          />
         </q-card-actions>
    </paystack>


      </q-card>

    </q-dialog>

    <!-- result -->

    <q-dialog v-model="result">
      <q-card>

        <q-card-section class="row">
          <q-btn
          class=""
          style="margin-left:240px;"
          v-close-popup
          icon="close"
          />
          <div class="text-h6 q-pa-md">Scheduled Appointment Status</div>

        </q-card-section>

<table style="margin-right:50px;"  v-if="Object.keys(appointments).length">
  <tr>
    <th>Special request</th>
    <th>Status</th>
    <th>Time</th>
    <th>Date</th>
    <th>Clinic</th>
  </tr>
  <tr v-for="appointment in appointments" :key="appointment.id">
    <td>{{appointment.complain}} </td>
    <td v-if="appointment.status != ''">{{appointment.status}}</td>
    <td v-if="appointment.status == ''">Pending</td>
    <td>{{appointment.realtime}}</td>
    <td>{{appointment.timestamp}}</td>
    <td>{{appointment.clinic}}</td>
  </tr>

</table>
        </q-card>

    </q-dialog>

    <!-- nurse [all admitted patients] -->

    <q-dialog v-model="a_a_p">
      <q-card>
        <q-card-section class="row">
          <div class="text-h6">All Admitted Patients</div>
          <q-space/>
          <q-btn
          v-close-popup
          icon="close"

          />
        </q-card-section>
        <p class="q-ml-md" style="margin-top:-20px;">Available bed space : {{bed_space}}</p>

    <table style="margin-right:50px;" v-if="Object.keys(aPatients).length">
  <tr>
    <th>Patient ID</th>
    <th>Admitted By</th>
    <th>Date Of Admission</th>
  </tr>
  <tr v-for="aPatient in aPatients" :key="aPatient.id">
    <td>{{aPatient.patient_id}} </td>
    <td>{{aPatient.admitted_by}}</td>
    <td>{{aPatient.date_of_admission}}</td>
  </tr>

</table>
 </q-card>

    </q-dialog>

    <!-- nurse [all patients request] -->

    <q-dialog v-model="respond">
      <q-card>
   <form @submit.prevent="">
        <q-card-section class="row">
          <div class="text-h6">All Patients Requests</div>
          <q-space/>
          <q-btn
          v-close-popup
          icon="close"

          />
        </q-card-section>
        <q-card-section>
          <div  class="q-mb-md">


          </div>
        </q-card-section>

         </form>
      </q-card>

    </q-dialog>

      <!-- nurses send broadcast -->
    <q-dialog v-model="s_b">
      <q-card>
   <form @submit.prevent="sendBroadcast">
        <q-card-section class="row">
          <div class="text-h6 p-md-a">Send Broadcast</div>
          <q-space/>
          <q-btn
          v-close-popup
          icon="close"

          />
        </q-card-section>

           <q-card-section>

          <div  class="q-mb-md">
                                     <q-banner style="margin:15% 0 0 23%; width:50%"
            v-if="msg"
            @click="msg = ''"
            class="q-mb-md bg-warning text-center fixed-top"
            >
            {{msg}}
            </q-banner>
          <q-input
          ref="title"
          required
          outlined
          v-model="broadcast_msg"
          label="message"
          >
          <template v-slot:append>
                <q-icon name="close"
                 class="cursor-pointer"

                 >
                </q-icon>
              </template>
          </q-input>

          </div>
            <div  class="q-mb-md">
            <q-input outlined v-model="broadcast_timestamp" label="date">
              <template v-slot:append>
                  <q-icon name="close"
                 class="cursor-pointer"
                 >
                </q-icon>

                <q-icon name="event" class="cursor-pointer">
                  <q-popup-proxy>
                    <q-date  v-model="broadcast_timestamp"/>
                  </q-popup-proxy>
                </q-icon>
              </template>
            </q-input>
          </div>
        </q-card-section>
          <q-card-actions  align="right">
        <q-btn
        type="submit"
          color="primary"
          label="send"
          />
         </q-card-actions>
         </form>
      </q-card>
    </q-dialog>
    <q-dialog v-model="u_f">
      <q-card>
   <form @submit.prevent="uFile">
        <q-card-section class="row">
          <div class="text-h6 q-pa-md">Upload Files</div>
          <q-space/>
          <q-btn
          v-close-popup
          icon="close"

          />
        </q-card-section>

           <q-card-section>

          <div  class="q-mb-md">
            <q-banner style="margin:15% 0 0 23%; width:50%"
            v-if="msg"
            @click="msg = ''"
            class="q-mb-md bg-warning text-center fixed-top"
            >
            {{msg}}
            </q-banner>
      <q-file outlined v-model="file">
        <template v-slot:prepend>
          <q-icon name="attach_file" />
        </template>
      </q-file>

          </div>

        </q-card-section>
      <q-card-actions  align="right">
        <q-btn
        type="submit"
          color="primary"
          label="upload"
          />
         </q-card-actions>
         </form>
      </q-card>
    </q-dialog>

    <!-- admin see appointment -->

    <q-dialog v-model="see_a">
      <q-card>
   <form @submit.prevent="">
        <q-card-section class="row">
          <div class="text-h6 p-md-a">All Appointments</div>
          <q-space/>
          <q-btn
          v-close-popup
          icon="close"

          />
        </q-card-section>
          <q-banner style="margin:15% 0 0 23%; width:50%"
            v-if="msg"
            @click="msg = ''"
            class="q-mb-md bg-warning text-center fixed-top"
            >
            {{msg}}
            </q-banner>
        <q-card-section style="margin:0 0 0 0;" class="q-pa-md" v-if="Object.keys(rAppointments).length">
      <q-list  bordered  v-for="rAppointment in rAppointments" :key="rAppointment.id">
       <q-item
      :class="rAppointment.status !='approved' ? 'bg-orange-1' : 'bg-green-1'"
      @click="uRAppointments(rAppointment)"
      clickable
      >

        <q-item-section>
          <q-item-label>
           {{rAppointment.complain}}
          </q-item-label>
        </q-item-section>

<div class="row">
  <div class="column">


        <q-item-section class="q-ml-md">
          <q-item-label caption >
           {{rAppointment.timestamp}}
          </q-item-label>

          <q-item-label v-if="rAppointment.timestamp" caption class="row justify-end">
            <q-icon name="event" size="14px" class=""/>
          <small> {{rAppointment.realtime}}  </small>

          </q-item-label>
        </q-item-section>
  </div>

</div>

      </q-item>

    </q-list>
        </q-card-section>

         </form>
      </q-card>

    </q-dialog>

    <!-- admin view all/send patient name -->

    <q-dialog v-model="s_all_p">
      <q-card>
        <q-card-section class="row">
          <div class="text-h6 q-mr-md">Send Patient Name
            <p class="caption" style="font-size:15px; color:green; margin-left:10px">
              patients who sent name</p></div>
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
        <q-card-section style="margin-top:-30px;" class="q-pa-md" v-if="Object.keys(sPatients).length">
      <q-list  style="background-color:#fff; width:100%" bordered  v-for="sPatient in sPatients" :key="sPatient.patient_id">
       <q-item
      @click="uSPatients(sPatient)"
      clickable
      >

        <q-item-section>
          <q-item-label>
           {{sPatient.first_name}}  {{sPatient.last_name}}
          </q-item-label>
        </q-item-section>

<div class="row">
  <div class="column">


        <q-item-section class="q-ml-md">
          <q-item-label caption >
           {{sPatient.sex}}
          </q-item-label>

          <q-item-label v-if="sPatient.reg_date" caption class="row justify-end">
            <q-icon name="event" size="14px" class=""/>
          <small> {{sPatient.reg_date}}  </small>

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

    <!-- admin see patients and book appointment -->

    <q-dialog v-model="booking">
      <q-card>
   <form @submit.prevent="">
        <q-card-section class="row">
          <div class="text-h6">Book Appointment</div>
          <q-space/>
          <q-btn
          v-close-popup
          icon="close"

          />
        </q-card-section>
        <q-card-section>
          <div  class="q-mb-md">
          <q-input
          ref="title"
          :rules="[val => !!val || 'this field is required']"
          autofocus
          outlined

          label="patient name"
          >
          <template v-slot:append>
                <q-icon name="close"
                 class="cursor-pointer"

                 >
                </q-icon>
              </template>
          </q-input>

          </div>
          <div  class="q-mb-md">
            <q-input outlined  label="date">
              <template v-slot:append>
                  <q-icon name="close"
                 class="cursor-pointer"
                 >
                </q-icon>

                <q-icon name="event" class="cursor-pointer">
                  <q-popup-proxy>
                    <q-date  />
                  </q-popup-proxy>
                </q-icon>
              </template>
            </q-input>
          </div>
            <div  >
            <q-input outlined  label="time" >
              <template v-slot:append>
                 <q-icon name="close"
                 class="cursor-pointer"
                  >
                </q-icon>

                <q-icon name="access_time" class="cursor-pointer">
                  <q-popup-proxy>
                    <q-time />
                  </q-popup-proxy>
                </q-icon>
              </template>
            </q-input>
            </div>
        </q-card-section>
         <q-card-actions  align="right">
        <q-btn
        type="submit"
          color="primary"
          label="book"
          />
         </q-card-actions>
         </form>
      </q-card>

    </q-dialog>

    <!-- doctor document patient info -->

    <q-dialog v-model="pInfo">
      <q-card>
   <form @submit.prevent="">
        <q-card-section class="row">
          <div class="text-h6 p-md-a">Document Patient Info</div>
          <q-space/>
          <q-btn
          v-close-popup
          icon="close"

          />
        </q-card-section>
        <q-card-section>
          <div  class="q-mb-md">
          <q-input
          ref="title"
          :rules="[val => !!val || 'this field is required']"
          autofocus
          outlined

          label="patient name"
          >
          <template v-slot:append>
                <q-icon name="close"
                 class="cursor-pointer"

                 >
                </q-icon>
              </template>
          </q-input>

          </div>
          <div  class="q-mb-md">
            <q-input outlined  label="information">
              <template v-slot:append>
                  <q-icon name="close"
                 class="cursor-pointer"
                 >
                </q-icon>


              </template>
            </q-input>
          </div>
        </q-card-section>
        <q-card-actions  align="right">
        <q-btn
        type="submit"
          color="primary"
          label="save"
          />
         </q-card-actions>
         </form>
      </q-card>

    </q-dialog>

    <!-- doctor request for investigation -->

    <q-dialog v-model="rInvestigation">
      <q-card>
   <form @submit.prevent="">
        <q-card-section class="row">
          <div class="text-h6 p-md-a">Request Investigation</div>
          <q-space/>
          <q-btn
          v-close-popup
          icon="close"

          />
        </q-card-section>
        <q-card-section>
          <div  class="q-mb-md">


          </div>
        </q-card-section>

         </form>
      </q-card>
    </q-dialog>

    <!-- doctor send prescription request -->

    <q-dialog v-model="sPrescription">
      <q-card>
   <form @submit.prevent="">
        <q-card-section class="row">
          <div class="text-h6 p-md-a">Send Prescription Request</div>
          <q-space/>
          <q-btn
          v-close-popup
          icon="close"

          />
        </q-card-section>
           <q-card-section>
          <div  class="q-mb-md">
          <q-input
          ref="title"
          :rules="[val => !!val || 'this field is required']"
          autofocus
          outlined

          label="infirmity"
          >
          <template v-slot:append>
                <q-icon name="close"
                 class="cursor-pointer"

                 >
                </q-icon>
              </template>
          </q-input>

          </div>
        </q-card-section>
          <q-card-actions  align="right">
        <q-btn
        type="submit"
          color="primary"
          label="send"
          />
         </q-card-actions>
         </form>
      </q-card>
    </q-dialog>

       <!-- doctor manage admitted patients -->

    <q-dialog v-model="m_a_patients">
      <q-card>
   <form @submit.prevent="">
        <q-card-section class="row">
          <div class="text-h6 p-md-a">Manage Admitted Patients</div>
          <q-space/>
          <q-btn
          v-close-popup
          icon="close"

          />
        </q-card-section>
        <q-card-section>
          <div  class="q-mb-md">
          </div>
        </q-card-section>
         </form>
      </q-card>
    </q-dialog>

         <!-- doctor send info to admin -->

    <q-dialog v-model="s_i_admin">
      <q-card>
   <form @submit.prevent="">
        <q-card-section class="row">
          <div class="text-h6 p-md-a">Send Info To Admin</div>
          <q-space/>
          <q-btn
          v-close-popup
          icon="close"

          />
        </q-card-section>
           <q-card-section>
          <div  class="q-mb-md">
          <q-input
          ref="title"
          :rules="[val => !!val || 'this field is required']"
          autofocus
          outlined

          label="information"
          >
          <template v-slot:append>
                <q-icon name="close"
                 class="cursor-pointer"

                 >
                </q-icon>
              </template>
          </q-input>

          </div>
        </q-card-section>
        <q-card-actions  align="right">
        <q-btn
        type="submit"
          color="primary"
          label="send"
          />
         </q-card-actions>
         </form>
      </q-card>
    </q-dialog>
        <q-dialog v-model="sname">
      <q-card>

        <q-card-section class="q-pt-none q-mt-md">
          {{msg}}
        </q-card-section>

        <q-card-actions align="right">
          <q-btn flat label="OK" color="primary" v-close-popup />
        </q-card-actions>
      </q-card>
    </q-dialog>

        <q-dialog v-model="sname">
      <q-card>

        <q-card-section class="q-pt-none q-mt-md">
          {{msg}}
        </q-card-section>

        <q-card-actions align="right">
          <q-btn flat label="OK" color="primary" v-close-popup />
        </q-card-actions>
      </q-card>
    </q-dialog>

    <q-dialog v-model="t_a">
      <q-card>
        <q-card-section class="row">
          <div class="text-h6 p-md-a">All Treated Appointments</div>
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

  </tr>
  <tr v-for="rAppointment in rAppointments" :key="rAppointment.id" v-if="rAppointment.status !='pending'">
    <td>{{rAppointment.patient_id}} </td>
    <td>{{rAppointment.complain}}</td>
    <td>{{rAppointment.status}}</td>
    <td>{{rAppointment.realtime}}</td>
    <td>{{rAppointment.timestamp}}</td>
    <td>{{rAppointment.clinic}}</td>


  </tr>

</table>
      </q-card>

    </q-dialog>
    <q-dialog v-model="p_a">
      <q-card>
        <q-card-section class="row">
          <div class="text-h6 p-md-a">All Pending Appointments</div>
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
  <tr v-for="rAppointment in rAppointments" :key="rAppointment.id" v-if="rAppointment.status =='pending'">
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
    <q-dialog v-model="a_p">
      <q-card>
        <q-card-section class="row">
          <div class="text-h6 p-md-a">All Patients</div>
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
    <th>Name</th>
    <th>Pat_Type</th>
    <th>Address</th>
    <th>Phone</th>
    <th>Age</th>
    <th>Sex</th>
    <th>Religion</th>
    <th>Reg Date</th>
  </tr>
  <tr v-for="patient in gAPatients" :key="patient.patient_id">

    <td>{{patient.first_name}} {{patient.middle_name}} {{patient.last_name}} </td>
    <td>{{patient.pat_type}}</td>
    <td>{{patient.address}}</td>
    <td>{{patient.phone}}</td>
    <td>{{patient.age}}</td>
    <td>{{patient.sex}}</td>
    <td>{{patient.religion}}</td>
    <td>{{patient.reg_date}}</td>
  </tr>

      </table>


      </q-card>
    </q-dialog>
  </q-layout>
</template>

<script>
const NAME = 'user_name';
const ID = 'user_id';
const PASSWORD = 'password';
const USER_TYPE = 'user_type';

import paystack from 'vue-paystack'
import { mapState, mapActions } from 'vuex'
import mixinOtherUserDetails from 'src/mixins/mixin-other-user-details.js'
import EssentialLink from 'components/EssentialLink'

export default {
  mixins: [mixinOtherUserDetails],
  computed:{
      reference(){
        let text = "";
        let possible = "ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789";

        for( let i=0; i < 10; i++ )
          text += possible.charAt(Math.floor(Math.random() * possible.length));

        return text;
      },
    ...mapState('store', ['userDetails']),
        title(){
          let c_path = this.$route.path;
          if(c_path == '/home'){
            return 'Ask Question Section'
          }
           else if(c_path == '/auth'){
            return 'Login/Register'
          }
           else if(c_path == '/doc'){
            return 'Chat With Admin'
          }
            else if(c_path == '/viewer'){
            return ' '
          }
            else if(c_path == '/login'){
            return 'Arubah Login'
          }
            else if(c_path == '/c_login'){
            return 'Login To Ask Question'
          }
             else if(c_path == '/admin'){
            return 'Welcome '
            }
             else if(c_path == '/patient'){
            return 'Welcome '
          }
            else if(c_path == '/doctor'){
            return 'Welcome '
          }
            else if(c_path == '/nurse'){
            return ' '
          }
           if(c_path.includes('/chat')){
            return this.otherUserDetails.name
          }
          else{
            return 'Chat With Users'
          }
        }
      },
  name: 'MainLayout',

  components: {
    EssentialLink, paystack
  },
  props:['tab'],
  data () {
    return {
      p_a : false,
      t_a : false,
      u_name : localStorage.getItem(NAME),
      u_id : localStorage.getItem(ID),
      user_type : localStorage.getItem(USER_TYPE),
      leftDrawerOpen: false,
      essentialLinks: [
        {
          title: 'Docs',
          caption: 'know more about us',
          icon: 'school',
          link: 'http://arubahspecialisthospital.com/arubah/index.php/pg/about_us'
        },

        {
          title: 'FAQ',
          caption: 'faq.arubah',
          icon: 'record_voice_over',
          link: 'http://arubahspecialisthospital.com/arubah/index.php/pg/about_us'
        },
        {
          title: 'Instagram',
          caption: '@ashcalabar',
          icon: 'rss_feed',
          link: 'https://www.instagram.com/ashcalabar'
        },
        {
          title: 'Facebook',
          caption: '@ashcalabar',
          icon: 'public',
          link: 'https://www.facebook.com/ashcalabar'
        },
      ],
      appointments:[{


      }],
      rAppointments:[{


      }],
        aPatients:[{

      }],
      bMsgs:[{

      }],
      sPatients:[{

      }],
      gAPatients:[{

      }],
      commen : '',
      paystackkey : "pk_test_xxxxxxxxxxxxxxxxxxxxxxx", //paystack public key
      email: '', // Customer email
      amount: Number(''), // in kobo
      appointment : false,
      comment : false,
      broadcast_msg : '',
      broadcast_timestamp: '',
      bed_space: '',
      dialog : false,
      result : false,
      confirm : false,
      request : false,
      payment : false,
      see_a : false,
      booking : false,
      s_all_p : false,
      a_a_p : false,
      a_p : false,
      s_b : false,
      respond : false,
      pInfo : false,
      rInvestigation : false,
      sPrescription : false,
      m_a_patients : false,
      s_i_admin : false,
      date : '',
      time : '',
      doctor_id: '',
      clinic:'',
      my_id : '',
      status : '',
      complain : '',
      msg : '',
      sname : false,
      success : false,
      contact : false,
      u_f : false,
      file : null,
      map : false,
       options: [
        'Burns And Plastics', 'Dental Clinic', 'General Surgeon Clinic', 'Nephrologist Clinic',
         'O AND G CLINIC','Pediatrics Clinic','Physiotherapy [physical therapy] Clinic',
         'Cardiologist Clinic','ENT [Otolaryngology] Clinic','Heamaologist','Neurologist Clinic',
         'Ophthalmologist And Optometrists Clinic','Orthopedic Clinic','Physician Clinic',
         'Radiology Clinic','Urologist Clinic'
      ]

    }
  },
  mounted(){
  // if(this.$route.path=='/patient'){setTimeout(this.$forceUpdate(), 5000)}
  // const saved = true
  // if (saved) {
  //   setTimeout(this.$forceUpdate(), 5000)
  //   this.u_name = localStorage.getItem(NAME)
  // }
  // setInterval(function() {
  // this.u_name = localStorage.getItem(NAME)
  // }, 5000)
    // if (localStorage.user_name) {
    //   this.u_name = localStorage.user_name;
    // }
  window.addEventListener('foo-key-localstorage-changed', (event) => {
    this.u_name = event.detail.storage;
  });

  window.addEventListener('user_id_event', (even) => {
    this.u_id = even.detail.storage;
    console.log(this.u_id)
  });

  window.addEventListener('user_type_event', (eve) => {
    this.user_type = eve.detail.storage;
    console.log(this.user_type)
    this.fetchAppointment();
  });

  this.aSentPatients();
  this.fetchAppointment();
  this.aAppointments();
  this.aAPatients();
  this.bedSpace();
  this.getBroadcast();
  this.showSuccess();
  this.g_a_patients();
},
 watch: {
    // u_name(newName) {
    //   localStorage.user_name = newName;
    // }
  },
   methods: {
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
      bUComment(rAppointment){
        this.comment = true
        this.id = rAppointment.appointment_id
        this.doctor_id = rAppointment.doctor_id
        this.patient_id = rAppointment.patient_id
        this.complain = rAppointment.complain
      },
      callback: function(response){
        console.log(response)
      },
      showSuccess(){
        if(localStorage.getItem(NAME)){
           this.success = true
        }
      },
      close: function(){
          console.log("Payment closed")
      },
      ...mapActions('store', ['logoutUser']),
      bedSpace(){
        fetch("https://app.arubahspecialisthospital.com/index.php?mobileloginservice/numberOfAvailableBedspace")
        .then(res => res.json())
        .then(res => {
          this.bed_space = res.bedRecords
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
      sendBroadcast(){
        if(this.broadcast_msg !=''){
        fetch("https://app.arubahspecialisthospital.com/index.php?mobileloginservice/sendMessageBroadcst", {
         method: "POST",
         body: JSON.stringify({
           message_body: this.broadcast_msg,
           message_timestamp: this.broadcast_timestamp,
           sender_id : this.u_id
         }),
         headers: {
           "Content-type": "text/html",
           'Accept': 'application/json'
            }
         })
        .then(res => res.text())
        .then(text => {
          console.log(text)
          this.broadcast_timestamp =''
          this.broadcast_msg =''
          this.msg = 'Success'
        })
         .catch(err => console.log(err));
        }
      },
      getBroadcast(){
      if(localStorage.getItem(ID) != ''){
        fetch("https://app.arubahspecialisthospital.com/index.php?mobileloginservice/getAllBroadcast")
        .then(res => res.json())
        .then(res => {
          this.bMsgs = res.messageRecords
          console.log(res)
        })
      }
      else{
        this.bMsgs = []
      }
      },
      aAPatients(){
        fetch("https://app.arubahspecialisthospital.com/index.php?mobileloginservice/allAdmittedPatient")
        .then(res => res.json())
        .then(res => {
          this.aPatients = res.admittedPatientRecords
          console.log(res)
        })
      },
      g_a_patients(){
        fetch("https://app.arubahspecialisthospital.com/index.php?mobileloginservice/getAllPatients")
        .then(res => res.json())
        .then(res => {
          this.gAPatients = res.patientRecords.slice(0, 5)
          console.log(this.gAPatients)
        })
      },
      u_g_a_patients(){
        fetch("https://app.arubahspecialisthospital.com/index.php?mobileloginservice/getAllPatients")
        .then(res => res.json())
        .then(res => {
          this.gAPatients = res.patientRecords
          // .slice(0, 5)
          console.log(this.gAPatients)
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
          this.msg = 'Successful'
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
      fetchAppointment(){
       if(this.u_id != ''){
        fetch("https://app.arubahspecialisthospital.com/index.php?mobileloginservice/getBookedAppointment/"+this.u_id)
        .then(res => res.json())
        .then(res => {
          this.appointments = res.patient_appointment
          console.log(res)
        })
       }
       else{
         this.appointments = []
       }
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
          this.msg = res
          this.aSentPatients();
          console.log(res)
        })
      },
      updatePatient(){
        if(this.u_id !=''){
        fetch("https://app.arubahspecialisthospital.com/index.php?mobileloginservice/updatePatient/"+this.u_id, {
         method: "POST",
         body: JSON.stringify({
           to_admin: 1
         }),
         headers: {
           "Content-type": "application/json"
            }
        })
        .then(res => res.text())
        .then(res => {
          console.log(res)
          this.msg = 'Name Sent Successfuly To Admin'
          this.sname = true
        })
        }
        else{
          this.msg = 'no user id detected, please pull down to update page'
          this.sname = true
        }
      },
      sendName(){
        this.$q.dialog({
        title: 'Confirm',
        message: 'proceed to send?',
        ok:{
          push : true
        },
        cancel:{
          color:'negative'
        },
        persistent:true }).onOk(() =>{
          // this.deleteTask(id)
        })
      },
      logout(){
         localStorage.removeItem(NAME)
         localStorage.removeItem(ID)
         localStorage.removeItem(USER_TYPE)

         this.u_name = '';
         this.u_id = '';
         this.user_type= '';

          // window.location.reload()
        // localStorage.setItem(NAME, '')
        // localStorage.setItem(ID, '')
        this.appointments=[];
        console.log(this.u_name)
        console.log(this.u_id)
        this.$router.push('/login')

      },
      bookAppointment(){
        if(this.clinic=="General Surgeon Clinic"){
          this.time = '5:00 pm'
        }
        else if(this.clinic=="ENT [Otolaryngology] Clinic"){
          this.time = '5:00 pm'
        }
        else if(this.clinic=="Urologist Clinic"){
          this.time = '12:00 pm'
        }
        if(this.time !='' && this.complain !='' && this.date !='' && this.u_id !=''){
        fetch("https://app.arubahspecialisthospital.com/index.php?mobileloginservice/bookAppointment", {
         method: "POST",
         body: JSON.stringify({
           doctor_id:'',
           clinic: this.clinic,
           patient_id: this.u_id,
           realtime: this.time,
           status: 'pending',
           complain: this.complain,
           timestamp: this.date
         }),
         headers: {
           "Content-type": "text/html",
           'Accept': 'application/json'
            }
         })
        .then(res => res.text())
        .then(text => {
          console.log(text)
          this.doctor_id =''
          this.time =''
          this.complain =''
          this.date =''
          this.msg = 'Appointment booked successfully'
          this.fetchAppointment();
        })
         .catch(err => console.log(err));
        }
        else{
          alert('please pull page down to refresh')
        }
      }
    },
}
</script>
<style lang="stylus">
  .q-toolbar
    .q-btn
      line-height: 1.2



  aside
    opacity: 1.0  !important
    width: 350px  !important
    transform: translateX(0px)
</style>
<style>
#draw{
    background-image:url('~assets/draw.png');
    height:100%;
    background-size:cover;
}
#hea{
    background-image:url('~assets/v_slide/viewer.jpg');
    background-repeat: no-repeat;
    background-size: cover;
}
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

#cap{
  font-size:17px;
}
#lab{
  font-size:20px;
}
</style>
