<template>
  <div id="app">
    <div class="container" style="text-align:center;">
      <h2 style="display: block; margin: 4rem auto 2rem auto; color: #fff;
       font-size: 2rem; font-weight: bold;">Using ZipCode like: 72427</h2>
      <div class="row">
        <div class="col-12">
          <div class="zipSec">
            <h2>Zip Code</h2>
            <input type="text" placeholder="ZipCode.." v-model="zipValue" />
            <span
              ><p>{{ zipCity }}</p></span
            >
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
<script>

const axios = require('axios');

export default {
  data() {
    return {
      zipValue: "",
      zipCity: ""
    };
  },
  watch: {
    zipValue() {
      this.zipCity = "";
      if (this.zipValue.length == 5) {
        this.getZipFunc();
      }
    }
  },
  methods: {
    getZipFunc() {
      this.zipCity = "Search..";
      axios
        .get("https://ziptasticapi.com/" + this.zipValue)
        .then(response => {
          this.zipCity = response.data.city;
        })
        .catch((e) => {
          alert("Syntax error<br/>" + e);
        });
    }
  }
};
</script>
