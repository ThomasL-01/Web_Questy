<template>
    <div class = "add-quest">
        <h2>Ajouter une nouvelle quête</h2>
        <form>
            <input type="text" placeholder="Nom de la quête"  v-model="name" required = true/>
            <br>
            <input type="text" placeholder="Description de la quête" v-model="desc"/>
            <br>
            <select v-model="difficulty" required = true>
              <option :value="1">⭐ Novice</option>
              <option :value="2">⭐⭐ Apprenti</option>
              <option :value="3">⭐⭐⭐ Vétéran</option>
              <option :value="4">⭐⭐⭐⭐ Héros</option>
              <option :value="5">⭐⭐⭐⭐⭐ Légendaire</option>
            </select>
            <br>
            <input type="number" placeholder="Récompense en XP" v-model="reward"/>
            <br>
            <input type="date" placeholder="Date limite" v-model="dateLimite"/>
            <br>
            <button type="submit" @click="$emit('add-card', {id: 0, name: this.name, desc: this.desc, difficulty: this.difficulty, reward: this.reward, status: 'Disponible', dateLimite: this.dateLimite })">Ajouter une quête</button>
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
    }
}
</script>

<style scoped> </style>