<template>
  <v-container>
    <v-row 
    class="text-center" 
    style="background-color: #8ecae6; min-height: 100vh"
    >
      <v-col cols="12">
      </v-col>
      <v-col class="mb-4">
        <router-link
        to="/"
        >
        <v-icon
          style="position:absolute; right: 15px; top: 15px;"
          class="textshadow white"
        >
        mdi-home
        </v-icon>
        </router-link>
        <h1 class="display-2 bold mb-3 white textshadow">
          AFM - AMKA
        </h1> <br>
        <v-card style="min-height: 50vh">
          <v-card-title>
            <h1 
            style="width: 100%; text-align:center;"
            >
            Settings
            </h1>
          </v-card-title>
          <v-card-text>
            <v-btn 
            @click="showAdd = !showAdd" 
            class="white" 
            style="background-color: blue"
            >
              Add
            </v-btn>
            <br>
            <br>
            <v-form 
            class="border radius boxshadow" 
            v-if="showAdd" 
            lazy-validation
            >
            <div>
            <v-col>
              <v-row>
                <v-col cols="3">
                  <p>Name</p>
                </v-col>
                <v-col>
                  <v-text-field
                  dense
                  v-model="name"
                  required
                  :rules="nameRules"
                  ></v-text-field>
                </v-col>
                </v-row>
              <v-row>
                <v-col cols="3">
                  <p>AFM</p>
                </v-col>
                <v-col>
                  <v-text-field
                  dense
                  v-model="afm"
                  :rules="afmRules"
                  ></v-text-field>
                </v-col>
                </v-row>
              <v-row>
                <v-col cols="3">
                  <p>AMKA</p>
                </v-col>
                <v-col>
                  <v-text-field
                  dense
                  v-model="amka"
                  :rules="amkaRules"
                  ></v-text-field>
                </v-col>
                </v-row>
            </v-col>
          </div>
          <v-btn 
          class="white" 
          style="background-color: blue"
          @click="addData()"
          :disabled="nodata"
          >Save</v-btn>
          <br><br>
          </v-form>
          </v-card-text>
          <div>
            <v-btn 
            @click="showEdit = !showEdit" 
            class="white" 
            style="background-color: red"
            v-if="myData.length > 0"
            >Edit</v-btn> 
            <br><br>
            <div v-if="showEdit">
            <div
            v-for="(data, i) in this.myData"
             :key="i" 
             class="border radius" 
             style="margin-left: 10px;margin-right: 10px; margin-bottom:10px">
              <v-row>
                <v-col class="bold black"><br>
                  <p>Name: {{data.name}}</p><br>
                  <p>AFM: {{data.afm}}</p><br>
                  <p>AMKA: {{data.amka}}</p><br>
                </v-col>
                <v-col cols="1">
                  <v-icon
                  style="right: 30px; color: red;"
                  class="textshadow"
                  @click="remove(i)"
                  >mdi-delete
                  </v-icon>
                </v-col>
              </v-row>
            </div><br>
          </div>
          </div>
        </v-card>
        <p class="bold" style="padding-top: 10px;">
          by <a href="https://cdpas.net" class="black bold">cdpas</a>
        </p>
      </v-col>
    </v-row>
  </v-container>
</template>
<script>
  export default {
    name: 'Settings',
    components: {
    },
    data () {
      return {
        name: '',
        afm: '',
        amka: '',
        myData: [],
        nodata: true,
        showAdd: false,
        showEdit: false,
        afmWrong: false,
        amkaWrong: false,
        nameRules: [
          v => !!v || 'Name is required',
          v => (v && v.length >= 3) || 'Name must be at least than 3 characters',
        ],
        afmRules: [
          v => (v && v.length >= 9) || 'AFM must be 9 digits long',
          v => (v && v.length <= 9) || 'Too long',
        ],
        amkaRules: [
          v => (v && v.length >= 11) || 'AMKA must be 11 digits long',
          v => (v && v.length <= 11) || 'Too long',
        ],
      }
    },
    methods: {
      addData() {
        if (localStorage.getItem("elPersonalData")) {
          this.myData = JSON.parse(localStorage.getItem("elPersonalData"));
        }
        var arrLen = this.myData.length;
        this.myData.push({id: (arrLen), name: this.name, afm: this.afm, amka: this.amka});
        localStorage.setItem("elPersonalData", JSON.stringify(this.myData));
        this.clear();
      },
      clear() {
        this.name = '';
        this.afm = '';
        this.amka = '';
      },
      remove(id) {
         this.$delete(this.myData, id);
         localStorage.setItem("elPersonalData", JSON.stringify(this.myData));
         this.myData = JSON.parse(localStorage.getItem("elPersonalData"));
      }
    },
    watch: {
      name: function() {
        this.name.length > 1 ? this.nodata = false : this.nodata = true; 
      },
      afm: function() {
        if (this.afm.length != 9) {
          this.afm.length == 0 ? this.nodata = false : this.nodata = true;
        } else {
            this.nodata = false;
          }
      },
      amka: function() {
        if (this.amka.length != 9) {
           this.amka.length == 0 ? this.nodata = false : this.nodata = true;
        } else {
            this.nodata = false;
          }
      }
    },
    mounted() {
      if (localStorage.getItem("elPersonalData")) {
          this.myData = JSON.parse(localStorage.getItem("elPersonalData"));
        }
    }
  }
</script>
<style scoped>
</style>