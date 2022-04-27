<template>
  <user-login v-if="!isValidated" @getUserId ="getUserId"/>
  <user-subscribe v-if="isValidated" :userid="currentUser"/>
</template>

<script>
import userSubscribe from "./components/subscribe.vue"
import userLogin from "./components/login.vue"

export default {
  name: 'App',
  components: {
    userSubscribe,
    userLogin
  },
  data () {
    return {
      isValidated : false,
      currentUser :null
    }
  },
  methods: {
    getUserId (userid) {
      if(userid){
        console.log(userid);
        this.currentUser = userid
        this.isValidated = true
        console.log(this.isValidated)
      }
    }

  }
}
</script>

<style>

</style>
