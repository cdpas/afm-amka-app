<template>
  <v-container>
    <v-row class="text-center" style="background-color: #8ecae6; min-height: 100vh">
      <v-col cols="12">
      </v-col>
      <v-col class="mb-4">
        <router-link
        to="/settings"
        >
        <v-icon
        class="textshadow white"
            style="position:absolute; right: 15px; top: 15px;"
            >mdi-cog</v-icon>
        </router-link>
        <h1 class="display-2 font-weight-bold mb-3 textshadow white">
          AFM - AMKA
        </h1> <br>
        <v-card>
          <div v-if="myData.length < 1">
            No Data registered <br>
            Please add Data in <router-link
        to="/settings"
        >Settings</router-link>
          </div>
          <v-tabs
            v-model="tab"
            background-color="#fb8500"
            class="white"
            dark
            v-if="myData.length > 0"
          >
            <v-tab
              v-for="item in myData"
              :key="item.tab"
              class="textshadow bold"
            >
              {{ item.name }}
            </v-tab>
          </v-tabs>
          <v-tabs-items v-model="tab">
            <v-tab-item
              v-for="item in myData"
              :key="item.name"
            >
              <v-card flat style="min-height:440px">
                <v-card-text class="bold" style="font-size: 20px">
                  <p style="color: black; font-size: 28px">{{item.name}}</p><br>
                  <div v-if="item.afm.length > 0">
                    <p style="margin-bottom: 0; color: black">AFM: {{item.afm}}</p>
                  <VueBarcode :value="item.afm" text=" ">
                    Not loaded
                  </VueBarcode>
                  <br>
                  </div>
                  <div v-if="item.amka > 0">
                    <p style="margin-bottom: 0; color: black">AMKA: {{item.amka}}</p>
                  <VueBarcode :value="item.amka" text=" ">
                    Not loaded
                  </VueBarcode>
                  </div>
                  </v-card-text>
              </v-card>
            </v-tab-item>
          </v-tabs-items>
        </v-card>
        <p class="bold" style="padding-top: 10px;">
          by <a href="https://cdpas.net" class="bold black">cdpas</a>
        </p>
      </v-col>
    </v-row>
  </v-container>
</template>
<script>
import VueBarcode from 'vue-barcode';
  export default {
    name: 'Home',
    components: {
    VueBarcode,
    },
    data () {
      return {
        tab: null,
        myData: []
      }
    },
    methods: {
    },
    mounted() {
      if (localStorage.getItem("elPersonalData")) {
          this.myData = JSON.parse(localStorage.getItem("elPersonalData"));
        }
    }
  }
</script>
<style scoped>
.v-tab {
  width: 100%!important
}
</style>