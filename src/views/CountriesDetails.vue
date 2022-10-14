<template>
    <section class="section" v-if="!isLoading">

        <figure class="image is-128x128">
            <img src="`https://flagpedia.net/data/flags/icon/72x54/${country.alpha2Code.toLowerCase()}.png`">
        </figure>
        <div class="title">{{country.name.common}}</div>
        <table class="table is-fullwidth">
            <tbody>
                <tr>
                    <td>Capital</td>
                    <td>{{country.capital[0]}}</td>
                </tr>
                <tr>
                    <td>Area</td>
                    <td>{{country.area}} km <sup>2</sup></td>
                </tr>
                <tr>
                    <td>Borders</td>
                    <td>
                        <ul>
                            <li v-for="borders in country.borders">
                            <router-link :to="{name: 'details', params: {code: border}}">
                                {{findCountry(border).name.common}}</router-link>
                            </li>
                        </ul>
                    </td>
                </tr>

            </tbody>
        </table>
    </section>
</template>
<script setup>
import {ref, onMounted} from 'vue'
import { useRoute } from 'vue-router'
import countries from '../assets/countries.json'

const route = useRoute();
const country = ref();
const isLoading = ref(true);

// es una funcion que es llamado en el momento que el componente esta listo
onMounted(() => {
    country.value = findCountry(route.params.code)
    console.log(country.value)
    isLoading.value = false;
})

watch(()=> route.params.code, newValue => {
    console.log('pais cambiado', newValue)
    paisInfo.value = findPais(route.params.pais)
})


const findCountry = (code) => {
    // esto nos va a buscar el pais en la array. COMO BUSCAR UN ELEMENTO EN UNA ARRAY
    return countries.find((country) => {
        return country.alpha3Code === code
    })
}
</script>
<style scoped>

</style>