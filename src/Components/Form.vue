<template>
    <div class = "add-quest">
      <form>
        <input type="text" placeholder="Nom de la quête"  @input="onInputName"/>
        <input type="text" placeholder="Description de la quête" @input="onInputDesc"/>
        <input type="number" placeholder="Niveau de difficulté" @input="onInputDifficulty"/>
        <input type="number" placeholder="Récompense en XP" @input="onInputReward"/>
        <input type="date" placeholder="Date limite" @input="onInputDateLimite"/>
        <button type="submit" @click="$emit('add-card', quest)">Ajouter une quête</button>
      </form>
    </div>
</template>

<script>
export default {
    emits: ['add-card'],   
    data () {
        return {
            name: '',
            desc: '',
            difficulty: null,
            reward: null,
            dateLimite: null
        }
    },
    methods:{
        // Méthodes pour gérer les entrées du formulaire
        onInputName(value) {
        this.name = value;
        },
        onInputDesc(value) {
        this.desc = value;
        },
        onInputDifficulty(value) {
        this.difficulty = value;
        },
        onInputReward(value) {
        this.reward = value;
        },
        onInputDateLimite(value) {
        this.dateLimite = value;
        },
    }
}
</script>

<style scoped> </style>