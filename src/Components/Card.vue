<template>
    <div class ="card">
        <h3>{{ name }}</h3>
        <p>{{ desc }}</p>
        <p> Niveau de difficulté : {{ difficulty }}</p>
        <p> statut : {{ status }}</p>
        <p> Récompense : {{ reward }} XP</p>
        <p> Date limite : {{ dateLimite }}</p>
        <button @click="$emit('delete-card', id)">Supprimer</button>
    </div>
</template>

<script>
export default { 
    emits: ['delete-card'],   
    props: {
        id : Number,
        name : String,
        desc : String,
        difficulty : Number,
        status : String,
        reward : Number,
        dateLimite : String
    },

};
</script>

<style scoped> </style>