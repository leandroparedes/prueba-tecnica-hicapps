<template>
    <div class="countries-select">
        <select @change="countryChanged($event)">

            <option disabled selected>Seleccione un país...</option>

            <option
                v-for="country in countries"
                :key="country.iso3"
                :value="country.iso3"
            >
                {{ country.name }}
            </option>

        </select>
    </div>
</template>

<script>
export default {
    name: 'CountriesSelect',

    data: function () {
        return { countries: [] }
    },

    mounted: function () {
        this.fetchCountries();
    },

    methods: {
        fetchCountries() {
            const url = process.env.VUE_APP_COUNTRIES_ENDPOINT;

            fetch(url).then(res => res.json()).then(res => {
                this.countries = res.countries;
            });
        },

        countryChanged: function (event) {
            const countryCode = event.target.value;

            this.$emit('country-changed', countryCode);
        }
    },
}
</script>

<style scoped>
    .countries-select {
        padding: 15px;
    }
</style>
