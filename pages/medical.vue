<template>
  <div class="medical">
    <navbar :activePage="activePage" />
    <div class="container shadow rounded-4 mt-4 p-3">
      <div class="tabs row text-center d-none d-sm-flex">
        <div class="col p-0">
          <h3 class=" btn btn-tab py-2" :class="counter == 0 ? 'active' : ''">Information</h3>
        </div>
        <div class="col p-0">
          <h3 class=" btn btn-tab py-2" :class="counter == 1 ? 'active' : ''">Upload</h3>
        </div>
        <div class="col p-0">
          <h3 class=" btn btn-tab py-2" :class="counter == 2 || counter == 3 ? 'active' : ''">Result</h3>
        </div>
      </div>
      <div class="content mt-4 text-center pb-4">
        <div v-if="counter == 0">
            <img src="@/assets/img/oie_5222240LGRJAcqG 1.png" class="img-fluid" alt="">
            <p class="section-title">You need to upload your</p>
            <h2 class="section-heading">Medical Test Result </h2>
            <p class="lead section-desc">
                              To can read your medical test, you must <br>
                              upload your medical test, So we put to you some <br>
                              options to can upload test .
            </p>
            <button class="btn-next-form btn mt-4 mx-auto" @click.prevent="counter++">Next</button>
        </div>
        <div v-if="counter == 1">
          <div class="container" style="margin-top: 5%;">
            <div class="row align-items-center">
              <div class="col-md-8 col-sm-12">
                <h2 class="text-black">To Upload Your test</h2>
                <div>
                  <input type="file" id="uploadFile" class="d-none" @change="onFileChange">
                  <label for="uploadFile" class="d-flex btn btn-upload w-25 m-auto">
                    <img src="@/assets/img/file.svg" class="img-fluid" alt="">
                    <h5 class="text-white" style="margin-left:8%;">Upload file / photo</h5>
                  </label>
                </div>
                <div id="preview" style="margin-top: 5%;">
                  <img v-if="showImage" :src="showImage" class="img-fluid border rounded p-3 shadow" style="width: 300px; height: 300px;"/>
                </div>
              </div>
              <div class="col-4 d-md-block d-none">
                <img src="@/assets/img/Doctor-rafiki 1.png" class="img-fluid" alt="">
              </div>
            </div>
            <button class="btn-next btn mt-4 w-15 d-block ml-auto" @click.prevent="counter++">Next</button>
          </div>
        </div>
        <div v-if="counter == 2">
          <div class="container result">
            <h2 class="text-black">You result is </h2>
            <img v-if="showImage" :src="showImage" class="img-fluid border rounded p-3 shadow mb-3" style="width: 300px; height: 300px;"/>
            <p class="text-left text-black">You May Suffer From</p>
            <h5>
              your body isn't getting enough oxygen, making you feel very tired and weak
              <ol class="mt-3 text-left">
                <li class="mb-2">
                  A person with reduced levels of hemoglobin may benefit from eating more iron-rich foods.
                </li>
                <li class="mb-2">
                  An insufficient supply of healthy red blood cells (anemia).
                  you may need to go to the doctor to get intravenous iron or blood transfusions.
                </li>
                <li class="mb-2">
                  A low red blood cell count increases the risk of anemia. Ways of boosting red blood cells include eating foods that contain iron, vitamin B12 and B9, vitamin C, vitamin A, and copper. Increasing exercise levels and reducing alcohol intake may also help.
                </li>
                <li class="mb-2">
                  your body is not making enough white blood cells. It can increase your risk of getting infections.
                  Lean meats, such as fish, eggs seafood, and skinless poultry contain high quantities of protein. Great plant based sources include lentils, beans and soy. Zinc is one of the best foods to increase white blood cells you can consume as it can help the body produce more WBCs and makes existing WBCs more aggressive.
                </li>
                <li class="mb-2">
                  you may have trouble stopping bleeding. Bleeding can happen inside your body, underneath your skin, or from the surface of your skin
                  your doctor can replace lost blood with transfusions of packed red blood cells or platelets
                </li>
              </ol>
            </h5>
            <div class="btns row">
                <div class="col-md-10">
                  <div class="row">
                    <div class="col-2 mt-4 col-btn"></div>
                    <div class="col-4 mt-4 col-btn">
                      <button class="btn btn-next">Save Your Result</button>
                    </div>
                    <div class="col-4 mt-4 col-btn">
                      <nuxt-link to="/" class="btn btn-next">Go back home</nuxt-link>
                    </div>
                    <div class="col-2 mt-4 col-btn"></div>
                    <div class="col-2 mt-4 col-btn"></div>
                    <div class="col-4 mt-4 col-btn">
                      <button class="btn btn-next" @click.prevent="counter--">Do another diagnosis test</button>
                    </div>
                    <div class="col-4 mt-4 col-btn">
                      <button class="btn btn-next" @click.prevent="counter++">Advanced options</button>
                    </div>
                    <div class="col-2 mt-4 col-btn"></div>
                  </div>
              </div>
              <div class="col-md-2 d-md-block d-none">
                <img src="@/assets/img/result1.png" alt="" class="img-fluid">
              </div>
            </div>
          </div>

        </div>
        <div v-if="counter == 3">
          <div class="container result">
            <h2 class="text-black">Advanced options </h2>
            <p class="text-left text-black">Advanced options like</p>
            <h5 class="text-left">
              <ul>
                <li>Know which doctor to go to </li>
                <li>Read you result with speech</li>
              </ul>
            </h5>
            <div class="btns d-flex align-items-end">
              <button class="btn btn-prev w-50 h-25"  @click.prevent="counter--">Back to result</button>
              <img src="@/assets/img/bitcoin.png" class="img-fluid" alt="">
              <button class="btn btn-next w-50 h-25" >Purchase for 99.9EGP </button>
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
      counter:0,
      showImage:null,
      activePage:'medical'
    }
  },
  methods:{
    onFileChange(e) {
      const file = e.target.files[0];
      this.showImage = URL.createObjectURL(file);
    }
  }
}
</script>

<style></style>
