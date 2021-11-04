<template>
  <GoogleLogin :params="params" :onSuccess="onSuccess" :onFailure="onFailure"
    >Login</GoogleLogin
  >
</template>
<script>
import GoogleLogin from 'vue-google-login';
//  import { LoaderPlugin } from 'vue-google-login';
 
//   Vue.use(LoaderPlugin, {
//         client_id: '447152703558-4jgcoc48kqag9e5b4d6vc5mjhcinvd8o.apps.googleusercontent.com'
//     });
//     Vue.GoogleAuth.then(auth2 => {
//         console.log(auth2.isSignedIn.get());
//         console.log(auth2.currentUser.get())
//     })
export default {
  name: "GoogleLogin",
  data() {
    return {
      // client_id is the only required property but you can add several more params, full list down bellow on the Auth api section
      params: {
        client_id:
          "447152703558-4jgcoc48kqag9e5b4d6vc5mjhcinvd8o.apps.googleusercontent.com",
      },
      // only needed if you want to render the button with the google ui
      renderParams: {
        width: 250,
        height: 50,
        longtitle: true,
      },
    };
  },
  components: {
    GoogleLogin,
  },
  methods: {
    onSuccess(googleUser) {
      console.log(googleUser);

      // This only gets the user information: id, name, imageUrl and email
      console.log(googleUser.getBasicProfile());
    },
  },
};
</script>
