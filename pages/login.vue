<template>
  <div>
    <navbar />
    <div class="login-form">
      <div class="container">
        <div class="row">
          <div class="col-md-6 d-md-block d-none">
            <img src="@/assets/img/Group 513552.png" class="img-fluid" alt="">
          </div>
          <div class="col-md-6">
            <form action="" class="bg-login" @submit.prevent="loginAction()">
              <h4>Login</h4>
              <p>Hello, Welcome Back To Your Account.</p>
              <div class="mt-4 mb-4">
                <label for="">Email Address</label>
                <input type="email" placeholder="EX.email@gmail.com" v-model="login.email" class="form-control">
              </div>
              <div class="mt-4 mb-4">
                <label for="">Password</label>
                <input type="password" placeholder="Enter your password" v-model="login.password" class="form-control">
              </div>
              <div class="d-flex" style="justify-content: space-evenly;">
                <div class="from-group">
                  <input type="checkbox" name="" id="remember">
                  <label for="remember">Remember Me</label>
                </div>
                <div class="forget">
                  <nuxt-link to="forgetpassword">Forget Password</nuxt-link>
                </div>
              </div>
              <button class="btn btn-login">Log in</button>
              <p class="text-center">Don't Have account? <nuxt-link to="/stepregister">Sign Up</nuxt-link></p>
            </form>
            <p class="text-center mt-2">--- OR ----</p>
            <div class="row mb-2">
              <div class="col-6">
                <button class="btn btn-loginSocial" @click.prevent="signInWithFacebook()">
                  <i class="fa-brands fa-facebook-f"></i> Login with Facebook
                </button>
              </div>
              <div class="col-6">
                <button class="btn btn-loginSocial" @click.prevent="signInWithGoogle()">
                  <i class="fa-brands fa-google"></i> Login with Google
                </button>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      login:{
        email:'',
        password:''
      }
    }
  },
  beforeMount(){
    if (localStorage.auth || localStorage.authFirebase) {
      this.$router.push('/');
      this.$toast.error("You Must logout To Make Login", {
            position: 'top-right',
            timeout: 2000,
            closeOnClick: true,
            pauseOnFocusLoss: true,
            pauseOnHover: true,
            draggable: true,
            draggablePercent: 0.6,
            showCloseButtonOnHover: false,
            hideProgressBar: true,
            closeButton: 'button',
            icon: 'fas fa-rocket',
            rtl: false
          })
    }
  },
  methods:{
    loginAction() {
      this.$axios
        .$post('http://localhost:8000/api/login', this.login)
        .then((res) => {
          console.log(res)
            this.$axios.setToken(res.token, 'Bearer')
            localStorage.setItem('auth', res.token)
            this.$router.push('/')
            this.$toast.success('Welcome ♥', {
            position: 'top-right',
            timeout: 2000,
            closeOnClick: true,
            pauseOnFocusLoss: true,
            pauseOnHover: true,
            draggable: true,
            draggablePercent: 0.6,
            showCloseButtonOnHover: false,
            hideProgressBar: true,
            closeButton: 'button',
            icon: 'fas fa-rocket',
            rtl: false
          })

        })
        .catch((error) => {
          console.log(error)
          this.$toast.error('Please Enter Correct Data', {
            position: 'top-right',
            timeout: 2000,
            closeOnClick: true,
            pauseOnFocusLoss: true,
            pauseOnHover: true,
            draggable: true,
            draggablePercent: 0.6,
            showCloseButtonOnHover: false,
            hideProgressBar: true,
            closeButton: 'button',
            icon: 'fas fa-rocket',
            rtl: false
          })
        })

      },
    async signInWithGoogle() {
      try{
        const provider = new this.$fireModule.auth.GoogleAuthProvider()
        // You can add or remove more scopes here provider.addScope('https://www.googleapis.com/auth/contacts.readonly');
        const authData = await this.$fire.auth.signInWithPopup(provider)
        console.log('authData')
        console.log(authData)
        localStorage.setItem('authFirebase',authData.credential.idToken)
        this.$router.push('/')
        this.$toast.success('Welcome ♥', {
              position: 'top-right',
              timeout: 2000,
              closeOnClick: true,
              pauseOnFocusLoss: true,
              pauseOnHover: true,
              draggable: true,
              draggablePercent: 0.6,
              showCloseButtonOnHover: false,
              hideProgressBar: true,
              closeButton: 'button',
              icon: 'fas fa-rocket',
              rtl: false
            })
      }
      catch(err){
        this.$toast.error(err, {
            position: 'top-right',
            timeout: 2000,
            closeOnClick: true,
            pauseOnFocusLoss: true,
            pauseOnHover: true,
            draggable: true,
            draggablePercent: 0.6,
            showCloseButtonOnHover: false,
            hideProgressBar: true,
            closeButton: 'button',
            icon: 'fas fa-rocket',
            rtl: false
          })
      }
    },
    async signInWithFacebook() {
      try {
        const provider = new this.$fireModule.auth.FacebookAuthProvider()
        // await auth.signInWithPopup(new firebase.auth.FacebookAuthProvider())
        const authData = await this.$fire.auth.signInWithPopup(provider)
        console.log('authData')
        console.log(authData)
      localStorage.setItem('authFirebase',authData.credential.idToken)
      this.$router.push('/')
      this.$toast.success('Welcome ♥', {
            position: 'top-right',
            timeout: 2000,
            closeOnClick: true,
            pauseOnFocusLoss: true,
            pauseOnHover: true,
            draggable: true,
            draggablePercent: 0.6,
            showCloseButtonOnHover: false,
            hideProgressBar: true,
            closeButton: 'button',
            icon: 'fas fa-rocket',
            rtl: false
          })

      } catch (err) {
        alert(err)
        this.$toast.error(err, {
            position: 'top-right',
            timeout: 2000,
            closeOnClick: true,
            pauseOnFocusLoss: true,
            pauseOnHover: true,
            draggable: true,
            draggablePercent: 0.6,
            showCloseButtonOnHover: false,
            hideProgressBar: true,
            closeButton: 'button',
            icon: 'fas fa-rocket',
            rtl: false
          })

      }
    },
  }
}
</script>

<style>

</style>
