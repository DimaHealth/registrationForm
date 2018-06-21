<template>
    <div id="app">
        <div class="register">
            <div class="register__head">
                <div class="register__title">New User</div>
                <div class="register__user-fields">
                    <div class="register__firstname">{{this.getFirstName}}</div>
                    <div class="register__lastname">{{this.getLastName}}</div>
                    <span>/</span>
                    <div class="register__login">{{this.getLogin}}</div>
                    <div class="register__mail">{{this.getEmail}}</div>
                </div>

            </div>
            <div class="register__sign">
                <div class="register__title">Sign up</div>
                <form @submit.prevent="checkFields" class="register__form">

                    <div class="register__fields">
                        <div class="register__fields-item" :class="checkFieldFull(fulllogin)">
                            <label for="login">login<span>*</span></label>
                            <input v-model="login" :class="" name="login" type="text" id="login">
                        </div>
                        <div class="register__fields-item" :class="checkFieldFull(fullemail)">
                            <label for="email">email<span>*</span></label>
                            <input v-model="email" name="email" type="text" id="email">
                        </div>
                        <div class="register__fields-item" :class="checkFieldFull(fullpassword)">
                            <label for="password">password<span>*</span></label>
                            <input v-model="password" name="password" type="password" id="password">
                        </div>
                        <div class="register__fields-row">
                            <div class="register__fields-item register__fields-item--short">
                                <label for="firstname">first name</label>
                                <input v-model="firstname" name="firstname" type="text" id="firstname">
                            </div>
                            <div class="register__fields-item register__fields-item--short">
                                <label for="lastname">last name</label>
                                <input v-model="lastname" name="lastname" type="text" id="lastname">
                            </div>
                        </div>
                        <div class="register__fields-row">

                            <div class="register__fields-item register__fields-item--short">
                                <label>country</label>
                                <v-select placeholder="Select" v-model="country" name="country" id="country"
                                          :options="this.countries"></v-select>
                            </div>
                            <div class="register__fields-item register__fields-item--short" :class="cityClass">
                                <label>city</label>
                                <v-select  placeholder="Select" v-model="city" name="city" id="city" :options="this.cities"></v-select>
                            </div>
                        </div>
                        <div class="register__fields-row">

                            <div class="register__fields-item register__fields-item--short">
                                <label>date of birth</label>
                                <date-picker v-model="dateofbirth" nane="" :lang="lang"></date-picker>
                            </div>
                            <div class="register__fields-item register__fields-item--short">
                                <label for="zip">zip code</label>
                                <input v-model="zipcode" id="zip" name="zip" type="text">
                            </div>
                        </div>
                    </div>
                    <div class="register__submit">
                        <button type="submit">sign up</button>
                    </div>
                </form>

            </div>
        </div>
    </div>
</template>

<script>
    import DatePicker from 'vue2-datepicker'
    import Vuex from 'vuex'
    import Vue from 'vue'

    Vue.use(Vuex)
    import vSelect from 'vue-select'

    const store = new Vuex.Store({
        state: {
            notes: [],
            country: "",
            city: "",
            login: "",
            email: "",
            password: "",
            firstname: "",
            lastname: "",
            dateofbirth: "",
            zipcode: "",
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
            },
            setLogin({commit}, login) {
                commit('SET_LOGIN', login)
            },
            setEmail({commit}, email) {
                commit('SET_EMAIL', email)
            },
            setFname({commit}, firstname) {
                commit('SET_FNAME', firstname)
            },
            setLname({commit}, lastname) {
                commit('SET_LNAME', lastname)
            },
            setDate({commit}, date) {
                commit('SET_DATE', date)
            },
            setCode({commit}, code) {
                commit('SET_CODE', code)
            },
            setPassword({commit}, password) {
                commit('SET_PASSWORD', password)
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
            },
            SET_LOGIN(state, login){
                state.login = login
            },
            SET_EMAIL(state, email){
                state.email = email
            },
            SET_FNAME(state, firstname){
                state.firstname = firstname
            },
            SET_LNAME(state, lastname){
                state.lastname = lastname
            },
            SET_DATE(state, dateofbirth){
                state.dateofbirth = dateofbirth
            },
            SET_CODE(state, zipcode){
                state.zipcode = zipcode
            },
            SET_PASSWORD(state, password){
                state.password = password
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
            },
            login(state){
                return state.login
            },
            email(state){
                return state.email
            },
            firstname(state){
                return state.firstname
            },
            lastname(state){
                return state.lastname
            },
            dateofbirth(state){
                return state.dateofbirth
            },
            zipcode(state){
                return state.zipcode
            },
            password(state){
                return state.password
            }
        },
        modules: {}
    })

    export default {
        name: 'App',
        components: {DatePicker, vSelect},
        store,
        data(){
            return {
                city: "",
                cityClass: "register__fields-item--disabled",
                country: "",
                login: "",
                fulllogin: false,
                email: "",
                fullemail: false,
                formSbm: false,
                password: "",
                fullpassword: false,
                completedForm: false,
                firstname: "",
                lastname: "",
                dateofbirth: "",
                zipcode: "",
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
            getFirstName(){
                return this.$store.getters.firstname.text
            },
            getLastName(){
                return this.$store.getters.lastname.text
            },
            getLogin(){
                return this.$store.getters.login.text
            },
            getEmail(){
                return this.$store.getters.email.text
            },
            cities(){
                if (!this.$store.getters.country) {
                    return []
                }
                return this.$store.getters.cities[this.$store.getters.country.text]
            },
            notes() {
                return this.$store.getters.notes;
            }
        },
        methods: {
            validEmail:function(email) {
                let re = /^(([^<>()\[\]\\.,;:\s@"]+(\.[^<>()\[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/;
                return re.test(email);
            },
            checkFieldFull(el){
                if (this.formSbm) {
                    return el ? "" : "register__fields-item--error"
                } else {
                    return ""
                }
            },
            addNew() {
                this.$store.dispatch('addNote', {text: 'новая заметка'})
            },
            checkForm(){
                this.completedForm = this.fulllogin && this.fullemail && this.fullpassword
            },
            checkFields() {

                this.formSbm = true
                if (this.completedForm) {
                    alert("Форма заполнена ")
                } else {
                    alert("Форма заполнена не корректно")
                }

            }
        },
        watch: {
            country: function (val) {
                this.$store.dispatch('setCountry', {text: val})
                console.log(val);
                this.cityClass = val ? "" : "register__fields-item--disabled"

                if (val !== null) {
                    this.$store.dispatch('setCity', {text: this.$store.getters.cities[val][0]})
                    this.city = this.$store.getters.cities[val][0]
                } else {
                    this.city = undefined
                    this.$store.dispatch('setCity', {text: ''})

                }
            },
            login: function (val) {
                this.$store.dispatch('setLogin', {text: val})
                this.fulllogin = val ? true : false
                this.checkForm()
            },
            email: function (val) {
                this.$store.dispatch('setEmail', {text: val})
                this.fullemail = this.validEmail(val)
                this.checkForm()
            },
            firstname: function (val) {
                this.$store.dispatch('setFname', {text: val})
            },
            lastname: function (val) {
                this.$store.dispatch('setLname', {text: val})
            },
            dateofbirth: function (val) {
                this.$store.dispatch('setDate', {text: val})
            },
            zipcode: function (val) {
                this.$store.dispatch('setCode', {text: val})
            },
            password: function (val) {
                this.$store.dispatch('setPassword', {text: val})
                this.fullpassword = val ? true : false
                this.checkForm()

            }
        },
        mounted: function () {
            this.login = this.$store.getters.login
            this.country = this.$store.getters.country
            this.city = this.$store.getters.city
            this.email = this.$store.getters.email
            this.firstname = this.$store.getters.firstname
            this.lastname = this.$store.getters.lastname
            this.dateofbirth = this.$store.getters.dateofbirth
            this.zipcode = this.$store.getters.zipcode
        },
    }
</script>

<style lang="sass">

    @import "./sass/register.sass";
    @import "./sass/base.sass";

</style>
