<template>
<div>
  <q-banner
    v-if="form_data.error"
    class="q-mb-md bg-warning text-center"
    >
    {{form_data.error}}
  </q-banner>
  <div class="flex flex-center q-mb-md" style="margin:0 0 5% 0">
    <img style="width:60%; margin-top:60px;"
      alt="Quasar logo"
      src="~assets/logo.png"
    >

</div>

  <q-form @submit="submit_form">
    <q-input
    outlined
    v-if="tab=='patient login'"
    style="background-color:white"
    required
    label="username"
    v-model="form_data.username"
    class="q-mb-md"
    />

    <q-input
    style="background-color:white"
    v-if="tab=='patient login'"
    outlined
    required
    label="password"
    v-model="form_data.password"
    class="q-mb-md"
    />

    <q-input
    v-if="tab=='staff login'"
    outlined
    label="your username"
    v-model="form_data.username"
    class="q-mb-md"
    />
    <q-input
    v-if="tab=='staff login'"

    outlined
    type="password"
    label="password"
    class="q-mb-md"
    v-model="form_data.password"
    />
    <div class="row">
      <q-space />
        <q-btn
        type="submit"
        color="primary"
        label="login"

        />
    </div>
  </q-form>
</div>
</template>

<script>

const NAME = 'user_name';
const ID = 'user_id';
const PASSWORD = 'password';
const USER_TYPE = 'user_type';

import { mapState, mapActions } from 'vuex'
import { mapGetters } from 'vuex'
export default {
computed: {
    ...mapGetters('store', ['errors'])
  },
    ...mapState('store', ['userDetails']),
props:['tab'],
data(){
  return{
    form_data:{
      username:'',
      password:'',
      error: ''
    }
  }
},
mounted(){
  // console.log($vmz.$store.state)
},
methods:{
  ...mapActions('store', ['registerUser', 'loginUser']),
  submit_form(){

    if(this.tab == 'patient login' || this.tab == 'staff login'){
      // this.p_s_login(this.form_data);
      fetch("https://app.arubahspecialisthospital.com/index.php?mobileloginservice/login", {
         method: "POST",
         body: JSON.stringify({
           username: this.form_data.username,
           password: this.form_data.password
         }),
         headers: {
           "Content-type": "application/json"
            }
         })
        .then(res => res.json())
        .then(res => {
          // console.log(localStorage.getItem(NAME))
          // console.log(res.loginRecords[0][0].user_id)
          if(!res.loginRecords){
              this.form_data.error = "this user credentials doesn't exist"
          }
          if(res.loginRecords[0][0].user_type == 'patient'){
            // localStorage.setItem(NAME, res.loginRecords[0][0].username)
            localStorage.setItem(ID, res.loginRecords[0][0].user_id)
            window.dispatchEvent(new CustomEvent('user_id_event', {
              detail: {
                storage: localStorage.getItem('user_id')
              }
            }));

            localStorage.setItem(USER_TYPE, res.loginRecords[0][0].user_type)
              window.dispatchEvent(new CustomEvent('user_type_event', {
              detail: {
                storage: localStorage.getItem('user_type')
              }
            }));

            localStorage.setItem(NAME, res.loginRecords[0][0].username)
            window.dispatchEvent(new CustomEvent('foo-key-localstorage-changed', {
              detail: {
                storage: localStorage.getItem('user_name')
              }
            }));

            this.$router.push('/patient')

          }
          else if(res.loginRecords[0][0].user_type == 'admin'){
            localStorage.setItem(ID, res.loginRecords[0][0].user_id)
            window.dispatchEvent(new CustomEvent('user_id_event', {
              detail: {
                storage: localStorage.getItem('user_id')
              }
            }));

            localStorage.setItem(USER_TYPE, res.loginRecords[0][0].user_type)
              window.dispatchEvent(new CustomEvent('user_type_event', {
              detail: {
                storage: localStorage.getItem('user_type')
              }
            }));

            localStorage.setItem(NAME, res.loginRecords[0][0].username)
            window.dispatchEvent(new CustomEvent('foo-key-localstorage-changed', {
              detail: {
                storage: localStorage.getItem('user_name')
              }
            }));
            this.$router.push('/admin')
          }
          else if(res.loginRecords[0][0].user_type == 'doctor'){
            localStorage.setItem(ID, res.loginRecords[0][0].user_id)
            window.dispatchEvent(new CustomEvent('user_id_event', {
              detail: {
                storage: localStorage.getItem('user_id')
              }
            }));

            localStorage.setItem(USER_TYPE, res.loginRecords[0][0].user_type)
              window.dispatchEvent(new CustomEvent('user_type_event', {
              detail: {
                storage: localStorage.getItem('user_type')
              }
            }));

            localStorage.setItem(NAME, res.loginRecords[0][0].username)
            window.dispatchEvent(new CustomEvent('foo-key-localstorage-changed', {
              detail: {
                storage: localStorage.getItem('user_name')
              }
            }));
            this.$router.push('/doctor')
          }
          else if(res.loginRecords[0][0].user_type == 'nurse'){
            localStorage.setItem(ID, res.loginRecords[0][0].user_id)
            window.dispatchEvent(new CustomEvent('user_id_event', {
              detail: {
                storage: localStorage.getItem('user_id')
              }
            }));

            localStorage.setItem(USER_TYPE, res.loginRecords[0][0].user_type)
              window.dispatchEvent(new CustomEvent('user_type_event', {
              detail: {
                storage: localStorage.getItem('user_type')
              }
            }));

            localStorage.setItem(NAME, res.loginRecords[0][0].username)
            window.dispatchEvent(new CustomEvent('foo-key-localstorage-changed', {
              detail: {
                storage: localStorage.getItem('user_name')
              }
            }));
            this.$router.push('/nurse')

          }
        }).catch(err => console.log(err));
      }
    }
  }
}
</script>

<style>

</style>
