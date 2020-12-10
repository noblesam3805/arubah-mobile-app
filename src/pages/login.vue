<template>
  <q-page class="flex q-pa-lg" style="padding-top:60px" id="nbg">
    <q-card class="full-width">
      <!-- <q-tabs
      dense
      v-model="tab"
      class="text-grey"
      align="justify"
      active-color="primary"
      indicator-color="primary"
      narrow-indicator

      >
      <q-tab name="patient login" color="white" label="patient login" id="nbg"/>
      <q-tab name="staff login" color="white" label="staff login" id="nbg"/>
      </q-tabs> -->
      <q-separator />
      <q-tab-panels v-model="tab" animated>

      <q-tab-panel name="patient login" id="nbg" style="height:650px;">
        <login :tab="tab"/>
      </q-tab-panel>

      <q-tab-panel name="staff login" id="nbg" style="height:450px;">
        <login :tab="tab"/>
      </q-tab-panel>
      </q-tab-panels>
    </q-card>
  </q-page>
</template>

<script>
export default {
  name: 'PageIndex',
  data(){
    return{
      tab:'patient login',
    }
  },
  components:{
    'login': require('components/login.vue').default
  }
}
</script>
<style>
  #nbg{
    background-image:url('~assets/v_slide/viewer.png');
    background-repeat: no-repeat;
    background-size: cover;
}
</style>
