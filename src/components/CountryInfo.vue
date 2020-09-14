<template>
    <div class="country-info">
        <div v-if="! loading">
            <h2>Situación COVID-19 en {{ countryCode }}</h2>
            <ul>
                <li>Confirmados: {{ confirmed }}</li>
                <li>Recuperados: {{ recovered }}</li>
                <li>Decesos: {{ deaths }}</li>
            </ul>
        </div>
        <p v-else>Cargando datos...</p>
    </div>
    
</template>

<script>
export default {
    props: {
        countryCode: {
            type: String,
            required: true
        }
    },

    data: function () {
        return {
            confirmed: 0,
            recovered: 0,
            deaths: 0,

            loading: false
        };
    },

    methods: {
        fetchCountryData(countryCode) {
            this.loading = true;

            const url = `${process.env.VUE_APP_COUNTRIES_ENDPOINT}/${countryCode}`;

            fetch(url).then(res => res.json()).then(res => {
                this.confirmed = res.confirmed.value;
                this.recovered = res.recovered.value;
                this.deaths = res.deaths.value;
            }).finally(() => this.loading = false);
        }
    },

    watch: {
        countryCode: {
            immediate: true,
            handler: function (countryCode) {
                this.fetchCountryData(countryCode);
            }
        }
    },
}
</script>

<style scoped>
    .country-info {
        padding: 40px;
    }
</style>