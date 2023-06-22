<template>
  <div>
    <navbar />
    <div class="login-form mt-2">
      <div class="container">
        <div class="row">
          <div class="col-md-6 d-md-block d-none align-self-center">
            <img src="@/assets/img/Group 513553.png" class="img-fluid" alt="">
          </div>
          <div class="col-md-6">
            <form action="" class="bg-login"  @submit.prevent="registerAction">
              <h4><nuxt-link to=""><i class="fa-solid fa-arrow-left"></i></nuxt-link> Create your account</h4>
              <div class="row">
                <div class="col-md-6 mt-1">
                    <label for="">First Name</label>
                    <div class="input-group">
                      <input type="text" placeholder="example" class="form-control" v-model="firstName">
                      <span class="input-group-text" id="basic-addon2"><i class="fa-solid fa-person"></i></span>
                    </div>
                </div>
                <div class="col-md-6 mt-1">
                  <label for="">Last Name</label>
                  <div class="input-group">
                    <input type="text" placeholder="example" class="form-control" v-model="lastName">
                    <span class="input-group-text" id="basic-addon2"><i class="fa-solid fa-person"></i></span>
                  </div>
                </div>
                <div class="col-md-12 mt-1">
                  <label for="">Email Address</label>
                  <input type="email" v-model="email" placeholder="EX.email@gmail.com" class="form-control">
                </div>
                <div class="col-12 mt-1">
                  <label for="">Phone Number</label>
                  <VuePhoneNumberInput v-model="phoneNumber" />
                </div>
                <div class="col-md-6 mt-1">
                  <label for="">Password</label>
                <div class="input-group">
                  <input v-if="showPassword" type="text" class="form-control" v-model="password" />
                  <input v-else type="password" class="form-control" v-model="password">
                  <button class="input-group-text btn" type="button" @click="toggleShow" id="basic-addon2"><i
                      class="fa-regular" :class="{ 'fa-eye-slash': showPassword, 'fa-eye': !showPassword }"></i></button>
                </div>
                </div>
                <div class="col-md-6 mt-1">
                  <label for="">Confirm Password</label>
                <div class="input-group">
                  <input v-if="reshowPassword" type="text" class="form-control" v-model="repassword" />
                  <input v-else type="password" class="form-control" v-model="repassword">
                  <button class="input-group-text btn" type="button" @click="toggleShowrepassword" id="basic-addon2"><i
                      class="fa-regular"
                      :class="{ 'fa-eye-slash': reshowPassword, 'fa-eye': !reshowPassword }"></i></button>
                </div>
                </div>
                <div class="col-md-6 mt-1">
                  <label for="">Age</label>
                  <div class="input-group">
                    <input type="date" placeholder="dd/mm/yyyy" v-model="age" class="form-control">
                  </div>
                </div>
                <div class="col-md-6 mt-1">
                  <label for="">Gender</label>
                  <div class="row">
                    <div class="col-md-6">
                      <input type="radio" id="male" value="0" name="gender" v-model="gender">
                      <label for="male">Male</label>
                    </div>
                    <div class="col-md-6">
                      <input type="radio" id="female" value="1" name="gender" v-model="gender">
                      <label for="female">Female</label>
                    </div>
                  </div>

                </div>
                <div class="col-md-6 mt-1">
                  <label for="">Do you Suffer from any disease ?</label>
                  <div class="input-group">
                    <input type="date" placeholder="dd/mm/yyyy" class="form-control" v-model="disease">
                  </div>
                </div>
                <div class="col-md-6 mt-1">
                  <label for="">Do you smoke cigarettes ?</label>
                  <div class="row">
                    <div class="col-md-6">
                      <input type="radio" id="yes" value="1" name="smoke" v-model="smoke">
                      <label for="yes">yes</label>
                    </div>
                    <div class="col-md-6">
                      <input type="radio" id="no" value="0" name="smoke" v-model="smoke">
                      <label for="no">No</label>
                    </div>
                  </div>
                </div>
              </div>
              <button class="btn btn-login">Sign Up</button>
              <p class="text-center">Do you Have account? <nuxt-link to="/login">Login</nuxt-link></p>
            </form>

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
      email:'',
      gender:null,
      smoke:null,
      age:'',
      firstName:'',
      lastName:'',
      name:'',
      disease:'',
      password: '',
      repassword: '',
      phoneNumber:null,
      showPassword: false,
      reshowPassword: false,
    }
  },
  beforeMount(){
    if (localStorage.auth || localStorage.authFirebase) {
      this.$router.push('/');
      this.$toast.error("You Must logout To Create New Account", {
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
  methods: {
    toggleShow() {
      this.showPassword = !this.showPassword;
    },
    toggleShowrepassword() {
      this.reshowPassword = !this.reshowPassword;
    },
    registerAction() {
      // eslint-disable-next-line prefer-const
      this.name=this.firstName + " " + this.lastName
      let registerForm = new FormData()
      registerForm.append('name', this.name)
      registerForm.append('email', this.email)
      registerForm.append('gender', this.gender)
      registerForm.append('mobile', this.phoneNumber)
      registerForm.append('password', this.password)
      registerForm.append('C_password', this.repassword)
      registerForm.append('disease', this.disease)
      registerForm.append('smoke', this.smoke)
      registerForm.append('age', this.age)
      console.log(registerForm)
      this.$axios
        .$post('http://localhost:8000/api/register', registerForm)
        .then((res) => {
          console.log(res)
          localStorage.setItem('auth', res.token)
          this.$router.push('/')

        })
    }
  },

}
</script>

<style>

</style>
