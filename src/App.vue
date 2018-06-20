<template >
  <div id="app">
    <div class="register">
      <div class="register__head">
        <div class="register__title">New User</div>
        <div class="register__firstname"></div>
        <div class="register__lastname"></div>
        <div class="register__login"></div>
        <div class="register__mail"></div>
      </div>
      <div class="register__sign">
          <div class="register__title">Sign up</div>
        <form class="register__form">

          <div class="register__fields">
            <div class="register__fields-item">
              <label for="login">login<span>*</span></label>
              <input name="login" type="text" id="login">
            </div>
            <div class="register__fields-item">
              <label for="email">email<span>*</span></label>
              <input name="email" type="text" id="email">
            </div>
            <div class="register__fields-item">
              <label for="password">password<span>*</span></label>
              <input name="password" type="password" id="password">
            </div>
            <div class="register__fields-item register__fields-item--short">
              <label for="firstname">first name</label>
              <input name="firstname" type="text" id="firstname">
            </div>
            <div class="register__fields-item register__fields-item--short">
              <label for="lastname">last name</label>
              <input name="lastname" type="text" id="lastname">
            </div>
            <div class="register__fields-item register__fields-item--short">
              <label >country</label>
              <v-select v-model="country"  name="country" id="country" :options="this.countries"></v-select>
            </div>
            <div class="register__fields-item register__fields-item--short">
              <label>city</label>
              <v-select v-model="city"  name="city" id="city" :options="this.cities"></v-select>
            </div>
            <div class="register__fields-item register__fields-item--short">
              <label>date of birth</label>
              <date-picker v-model="value" nane="" :lang="lang"></date-picker>
            </div>
            <div class="register__fields-item register__fields-item--short">
              <label for="zip">zip code</label>
              <input id="zip" name="zip" type="text">
            </div>
          </div>
          <div class="register__submit">
            <button type="submit">sign up</button>
          </div>
        </form>

      </div>
    </div>

    <!--<img src="./assets/logo.png">-->
    <!--<div  v-bind="index" v-for='note in notes'>-->
      <!--<div>-->
        <!--{{ note.text }}-->

      <!--</div>-->
    <!--</div>-->
    <!--<button @click='addNew'>Добавить заметку</button>-->
  </div>
</template>

<script>
import DatePicker from 'vue2-datepicker'
import Vuex from 'vuex'
import Vue from 'vue'

Vue.use(Vuex)

  const store = new Vuex.Store({
      state: {
          notes: [],
          country: "",
          city: "",
          countries: [
                "Russia",
                "Italy",
                "Germany"
          ],
          cities: {
              "Russia": [
                  "Rostov",
                  "Krasnodar",
                  "Taganrog"
              ],
              "Italy": [
                  "Verona",
                   "Milan",
                   "Florence"
              ],
              "Germany": [
                  "Berlin",
                  "Munhen",
                  "Frankfurt"
              ]
          }

      },
      actions: {
          setCountry({commit}, country) {
              commit('SET_COUNTRY', country)
          },
          setCity({commit}, city) {
              commit('SET_CITY', city)
          }
      },
      mutations: {
          ADD_NOTE(state, note) {
              state.notes.push(note)
          },
          SET_COUNTRY(state, country){
              state.country = country
          },
          SET_CITY(state, city){
              state.city = city
          }
      },
      getters: {
          countries(state){
              return state.countries
          },
          country(state){
              return state.country
          },
          cities(state){
              return state.cities
          }
      },
      modules: {}
  })

export default {
  name: 'App',
  components: { DatePicker },
  store,
  data(){
    return{
        city: "",
        showCity: false,
        country: "",
        value: '',
        lang: {
            days: ['Sun', 'Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat'],
            months: ['Jan', 'Feb', 'Mar', 'Apr', 'May', 'Jun', 'Jul', 'Aug', 'Sep', 'Oct', 'Nov', 'Dec'],
            pickers: ['next 7 days', 'next 30 days', 'previous 7 days', 'previous 30 days'],
            placeholder: {
                date: 'Select Date',
                dateRange: 'Select Date Range'
            }
        }
    }
  },
    computed: {
        countries(){
            return this.$store.getters.countries
        },
        cities(){
            if(!this.showCity){
                return []
            }
            console.log(this.$store.getters.cities[this.$store.getters.country.text]);
            return this.$store.getters.cities[this.$store.getters.country.text]
        },
        notes() {
            return this.$store.getters.notes;
        }
    },
    methods: {
        addNew() {
            this.$store.dispatch('addNote', { text: 'новая заметка' })
        }
    },
    watch: {
        country: function (val) {
            this.$store.dispatch('setCountry', { text: val })

            if(val !== null){
                this.showCity = true
                this.$store.dispatch('setCity', { text: this.$store.getters.cities[val][0] })
                this.city = this.$store.getters.cities[val][0]
            }else {
                this.city = ''
                this.$store.dispatch('setCity', { text: '' })

            }
        },
    },

    mounted: function(){
        console.log('mounted()', this);
    },
}
</script>

<style lang="sass" >

  @import "./sass/register.sass";
  @import "./sass/base.sass";

</style>
