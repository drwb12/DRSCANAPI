<template>
  <div>
    <navbar />
    <div class="forget-chooce">
      <div class="container">
        <div class="row">
          <div class="col-md-6 d-md-block d-none">
            <img src="@/assets/img/Group 513553.png" class="img-fluid" alt="">
          </div>
          <div class="col-md-6 align-self-center">
            <h3>Forget your password ?</h3>
            <p>Don’t Worry!  Its Happens. Please choose one option to reset your account.</p>
            <nuxt-link to="register" class="btn btn-send">Create new account </nuxt-link>
            <button @click.prevent="signInWithGoogle" class="btn btn-send"><i class="fa-brands fa-google"></i>  Sign-up with google  </button>
            <button @click.prevent="signInWithFacebook" class="btn btn-send"><i class="fa-brands fa-facebook-f"></i> Sign-up with facebook   </button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
methods:{
  async signInWithGoogle() {
      const provider = new this.$fireModule.auth.GoogleAuthProvider()
      const authData = await this.$fire.auth.signInWithPopup(provider)
      console.log('authData')
      console.log(authData)
      localStorage.setItem('authFirebase',authData.credential.idToken)
      this.$router.push('/')

    },
    async signInWithFacebook() {
      try {
        const provider = new this.$fireModule.auth.FacebookAuthProvider()
        const authData = await this.$fire.auth.signInWithPopup(provider)
        console.log('authData')
        console.log(authData)
      localStorage.setItem('authFirebase',authData.credential.idToken)
      this.$router.push('/')

      } catch (err) {
        alert(err)
      }
    },


}
}
</script>

<style>

</style>
