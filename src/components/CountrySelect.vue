<template>
    <select v-model="selected"
            @change="onChange"
            class="form-select mt-10 mb-5 block w-full border rounded">
        <option value="0">Select a Country</option>
        <option v-for="(country, i) of countries" :key="i" :value="country.ID">{{ country.Country}}</option>
    </select>
</template>

<script>

export default {
    name: "CountrySelect",
    props: [ 'countries' ],
    data () {
        return {
            selected: 0
        }
    },
    methods: {
        onChange () {
            const country = this.countries.find((item) => item.ID === this.selected)
            this.$emit('get-country', country)
        }
    }
}
</script>
