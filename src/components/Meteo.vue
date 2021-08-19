<template>
    <div class="container">
        <h1 class="my-4">la page météo avec Vue.js</h1>
        <div class="form-group mb-5">
            <label for="position">Entrez le nom d'une ville</label>
            <input 
            id="position" 
            type="text"
            class="form-control"
            v-model="requete"
            v-on:keypress="checkMeteo"
            >
        </div>

        <div class="w-75 m-auto" v-if="temps">
            <h3 class="text-center mb-3">Position : {{ temps.name }}</h3>
            <div class="card text-center p-5">
                <p class="texte-affichage">
                    Température : {{ temps.main.temp.toFixed()}}°C
                </p>
                <p class="texte-affichage">
                    Temps: {{temps.weather[0].description}}
                </p>
            </div>
        </div>    
    </div>
</template>

<script>

import axios from 'axios'

    export default {
        name: 'Meteo',
        data(){
            return {
                requete: '',
                temps: undefined,
                api_code:'07812679f5b87a3fa5bba83ce8255176',
                search_url: 'https://api.openweathermap.org/data/2.5/weather?',
            }
        },
        methods: {
            checkMeteo(e) {
                if(e.key == "Enter") {
                    axios
                    .get(`${this.search_url}q=${this.requete}&units=metric&appid=${this.api_code}&lang=fr`)
                    .then(reponse => {
                        // console.log(reponse.data);
                        this.temps = reponse.data;
                        console.log(this.temps);
                    })
                    this.requete = ''
                }
            }
        }
    }
</script>

<style>
    .texte-affichage {
        font-size: 1.5em;
        font-weight: 300;
        line-height: 1.2;
    }
</style>