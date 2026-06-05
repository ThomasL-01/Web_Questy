<template>
    <div class ="card">
        <h3>{{ name }}</h3>
        <p>{{ desc }}</p>
        <p v-if="difficulty == 1" class = "easy">⭐</p>
        <p v-if="difficulty == 2" class = "easy">⭐ ⭐</p>
        <p v-if="difficulty == 3" class = "medium">⭐ ⭐ ⭐</p>
        <p v-if="difficulty == 4" class = "hard">⭐ ⭐ ⭐ ⭐</p>
        <p v-if="difficulty == 5"class = "hard">⭐ ⭐ ⭐ ⭐ ⭐</p>
        <button v-if="status== 'Disponible'" @click="$emit('update-status', [id, 'En cours'])">Passer en cours</button>
        <button v-if="status == 'En cours'" @click="$emit('update-status', [id, 'Terminée'])">Passer en terminée</button>
        <p> Récompense : {{ reward }} XP</p>
        <p> Date limite : {{ dateLimite }}</p>
        <button @click="$emit('delete-card', id)">Supprimer</button>
    </div>
</template>

<script>
export default { 
    emits: ['delete-card', 'update-status'],   
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

<style scoped>
</style>