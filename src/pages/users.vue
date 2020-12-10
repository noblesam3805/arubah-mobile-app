<template>
  <q-page class="flex q-pa-md">
    <!-- <img
      alt="Quasar logo"
      src="~assets/quasar-logo-full.svg"
    > -->
    <q-list class="full-width" separator v-for="(users, key) in user"
  	  	:key="key">
      <q-item
       class="q-my-sm"
       :to="'/chat/' + key"
      clickable v-ripple>
        <q-item-section avatar >
          <q-avatar color="primary" text-color="white">
            {{ users.name}}
          </q-avatar>
        </q-item-section>

        <q-item-section >
          <q-item-label>{{ users.name }}</q-item-label>
        </q-item-section>

        <q-item-section side >
            <q-badge :color ="users.online ? 'light-green-5' : 'grey-4'">
            {{users.online ? 'online' : 'offline'}}
            </q-badge>
        </q-item-section>
      </q-item>
      <!-- <q-item v-else style="display:none; height:0px"/> -->

      <q-separator />

    </q-list>
  </q-page>
</template>

<script>
import { mapGetters } from 'vuex'

export default {
  data(){
    return{
      user:[{

      }]
    }
  },
  computed: {
    ...mapGetters('store', ['users'])
  },
  mounted(){
    this.user = this.users
    console.log(this.user)
  }
}

</script>
