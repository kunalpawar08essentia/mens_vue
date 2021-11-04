<template>
    <facebook-login class="button"
      appId="326022817735322"
      @login="getUserData"
      @logout="onLogout"
      @get-initial-status="getUserData">
      hello
    </facebook-login>

</template>


<script>
import facebookLogin from 'facebook-login-vuejs';
 
export default {
  name: "facebook",
  components: { facebookLogin},
  data(){
    return{
      idImage, loginImage, mailImage, faceImage,
      isConnected: false,
      name: '',
      email: '',
      personalID: '',
      FB: undefined
    }
  },
  methods: { 
  getUserData() {
      this.FB.api('/me', 'GET', { fields: 'id,name,email' },
        userInformation => {
          console.warn("data api",userInformation)
          this.personalID = userInformation.id;
          this.email = userInformation.email;
          this.name = userInformation.name;
        }
      )
    },
    sdkLoaded(payload) {
      this.isConnected = payload.isConnected
      this.FB = payload.FB
      if (this.isConnected) this.getUserData()
    },
    onLogin() {
      this.isConnected = true
      this.getUserData()
    },
    onLogout() {
      this.isConnected = false;
    }
  }
}
</script>
