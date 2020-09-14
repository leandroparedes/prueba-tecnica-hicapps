<template>
    <div id="app">
        <h1 class="title">COVID-19 Explorer</h1>
        
        <hr>
        
        <countries-select
            @country-changed="handleCountryChange"
        ></countries-select>
        
        <hr>
        
        <country-info
            v-if="selectedCountry"
            :country-code="selectedCountry"
        ></country-info>
    </div>
</template>

<script>
import CountriesSelect from './components/CountriesSelect.vue'
import CountryInfo from './components/CountryInfo.vue';

export default {
    name: 'App',

    components: {
        CountriesSelect,
        CountryInfo
    },

    data: function () {
        return { selectedCountry: null }
    },

    methods: {
        handleCountryChange: function (countryCode) {
            this.selectedCountry = countryCode;
        }
    }
}
</script>

<style>
    #app {
        font-family: Avenir, Helvetica, Arial, sans-serif;
        min-height: 100vh;
        background-color: #e87a63;
        color: #fff;
        padding: 30px;
    }

    .title {
        text-align: center;
    }
</style>
