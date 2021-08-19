<template>
    <div>
        <h1>Bienvue sur Page 2</h1>
        <div v-on:click="goAccueil" class="btn btn-warning">Retour au début</div>    
    </div>
</template>

<script>
    export default {
        name: 'Page2',
        methods: {
            goAccueil: function(){
                this.$router.push('/')
            }
        }
    }
</script>

<style>

</style>