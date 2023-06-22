<template>
  <div>
    <b-navbar toggleable="lg">
      <b-navbar-brand href="#"><img src="@/assets/img/logo.png" class="img-fluid" alt=""></b-navbar-brand>

      <b-navbar-toggle target="nav-collapse"></b-navbar-toggle>

      <b-collapse id="nav-collapse" is-nav>
        <b-navbar-nav>
          <li class="nav-item">
            <nuxt-link class="nav-link" :class="activePage=='Home'? 'active': ''" to="/">Home</nuxt-link>
          </li>
          <li class="nav-item">
            <nuxt-link class="nav-link" :class="activePage==''? 'active': ''" to="">About Us</nuxt-link>
          </li>
          <li class="nav-item">
            <nuxt-link class="nav-link" :class="activePage==''? 'active': ''" to="">Services</nuxt-link>
          </li>
          <li class="nav-item">
            <nuxt-link class="nav-link" :class="activePage=='diagnosis'? 'active': ''" to="/diagnosis">Diagnosis</nuxt-link>
          </li>
          <li class="nav-item">
            <nuxt-link class="nav-link" :class="activePage=='medical'? 'active': ''" to="medical">Medical Analysis</nuxt-link>
          </li>
          <li class="nav-item">
            <nuxt-link class="nav-link" v-if="auth" :class="activePage=='save'? 'active': ''" to="save">Saved Resulats</nuxt-link>
          </li>
          <li class="nav-item">
            <nuxt-link class="nav-link" v-if="auth" :class="activePage=='setting'? 'active': ''" to="settings">Settings</nuxt-link>
          </li>
        </b-navbar-nav>

        <!-- Right aligned nav items -->
        <b-navbar-nav class="ml-auto" v-if="!auth">
          <nuxt-link class="btn text-primary p-2 px-4 " to="login">Login</nuxt-link>
          <nuxt-link class="btn text-primary p-2 px-4" style="margin-left: 2;" to="stepregister">Register</nuxt-link>
      </b-navbar-nav>
        <b-navbar-nav class="ml-auto" v-else>
          <button type="button" class="btn btn-outline-danger" @click.prevent="logout()"><i class="fa-solid fa-right-from-bracket"></i></button>
      </b-navbar-nav>
</b-collapse>
    </b-navbar>

  </div>
</template>
<script>
export default {
  data() {
    return {
      auth:false,
    }
  },
  beforeMount(){
    if(localStorage.auth || localStorage.authFirebase){
    this.auth=true
    }
  },
  methods: {
    logout(){
      if(localStorage.auth){
        localStorage.removeItem('auth')
        this.$router.push('/')
        this.auth=false
      }else if(localStorage.authFirebase){
        localStorage.removeItem('authFirebase')
        this.$router.push('/')
        this.auth=false
      }
    }
  },
  props:['activePage'],
}
</script>
