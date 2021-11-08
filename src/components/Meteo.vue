<template>

    <div class="container">

        <h1 class="my-4">App météo avec Vue.js</h1>

        <div class="form-groupe mb-5">
            <label for="position">Entrez le nom d'une ville</label>
            <!-- une autre option de vueJS consiste à ajouter ".enter" a la suite de "v-on:keypress" pour eviter d'ajouter la condition if(e.key == "Enter") à la methods goMeteo -->
            <input type="text" id="position" class="form-control" v-model="requete" v-on:keypress="goMeteo">
        </div>
        <!-- on affiche cette partie seulement si on recois des donnée avec temps en faisant v-if="temps" -->
        <div class="w-75 m-auto" v-if="temps">
            <h3 class="text-center mb-3">Position : {{ temps.name }}</h3>
            <div class="card text-center p-5">
                <p class="texte-affichage">
                    <!-- toFixed() pour arrondir à l'entier sup -->
                    Température : {{ temps.main.temp.toFixed() }}
                </p> 
                <p class="texte-affichage">
                    Temps : {{ temps.weather[0].description }}
                </p>
            </div>
        </div>

    </div>

</template>


<script>
//axios pour faire des requettes http
import axios from 'axios'

export default {
    name: 'Meteo',
    data(){
        return {
            //une donnée requete inséré via l'imput v-model
            requete: '',
            //une donnée du temps qui est a défaut undefined
            temps: undefined,
            //les liens API code et url pour les requetes
            api_code: '1e1b5f883593813da8a64bd81e29d4d4',
            url_recherche: 'https://api.openweathermap.org/data/2.5/weather?'
        }
    },
    methods: {
        goMeteo(e){
            //si tu appuis sur Entrée alors....
            if(e.key == "Enter"){
                //on lance la requète, on prend via l'url (url_recherche) la requete (q) on demande en degres celcius(units=metric) avec la clé api (api_code) et en francais (lang=fr)
                axios
                .get(`${this.url_recherche}q=${this.requete}&units=metric&APPID=${this.api_code}&lang=fr`)
                //quand on a recu les réponses
                .then(reponse=>{
                    console.log(reponse)
                    this.temps = reponse.data;
                    console.log(this.temps.name)
                })
                //vider le champs de recherche une fois celle-ci effectué
                this.requete = ''
            }
        }
    },

}
</script>
<style>
.texte-affichage{
    font-size: 30px;
    font-weight: 300;
    line-height: 1.2;
}
</style>