<template>
    <div class = "add-quest">
        <h2 class="add-quest__title">Ajouter une nouvelle quête</h2>
        <form class="add-quest__form">
            <div class="form-row">
                <label class="form-label">Nom de la quête</label>
                <input type="text" placeholder="Nom de la quête"  v-model="name" required = true/>
            </div>
            <div class="form-row">
                <label class="form-label">Description</label>
                <input type="text" placeholder="Description de la quête" v-model="desc"/>
            </div>
            <div class="form-row form-row--inline">
                <div class="form-field">
                    <label class="form-label">Difficulté</label>
                    <select v-model="difficulty" required = true>
                        <option :value="1">⭐ Novice</option>
                        <option :value="2">⭐⭐ Apprenti</option>
                        <option :value="3">⭐⭐⭐ Vétéran</option>
                        <option :value="4">⭐⭐⭐⭐ Héros</option>
                        <option :value="5">⭐⭐⭐⭐⭐ Légendaire</option>
                    </select>
                </div>
                <div class="form-field">
                    <label class="form-label">Date limite</label>
                    <input type="date" placeholder="Date limite" v-model="dateLimite"/>
                </div>
            </div>
            <button type="submit" class="btn btn--accept" @click="$emit('add-card', {id: 0, name: this.name, desc: this.desc, difficulty: this.difficulty, reward: this.reward, status: 'Disponible', dateLimite: this.dateLimite })">Ajouter une quête</button>
        </form>
    </div>
</template>
<script>
export default {
    emits: ['add-card'],   // Événement émis pour ajouter une nouvelle quête
    data () {
        return { // On initialise les champs du formulaire
            name: '',
            desc: '',
            difficulty: null,
            dateLimite: null
        }
    }
}
</script>
<style scoped>
.add-quest {
    max-width: 700px;
    margin: 1rem auto 3rem;
    background: var(--color-parchment);
    color: var(--color-ink);
    padding: 1.75rem 2rem;
    border-radius: 3px;
    box-shadow: 0 10px 25px rgba(0,0,0,0.45), 0 0 0 6px rgba(0,0,0,0.08) inset;
    position: relative;
}

.add-quest::before {
    content: '';
    position: absolute;
    inset: 8px;
    border: 1px dashed var(--color-parchment-shadow);
    pointer-events: none;
}

.add-quest__title {
    font-family: var(--font-display);
    text-align: center;
    color: var(--color-rust-dark);
    margin: 0 0 1.25rem;
    font-size: 1.6rem;
}

.add-quest__form { display: flex; flex-direction: column; gap: 1rem; position: relative; }

.form-row { display: flex; flex-direction: column; gap: 0.3rem; }

.form-row--inline {
    flex-direction: row;
    flex-wrap: wrap;
    gap: 1rem;
}
.form-row--inline .form-field { flex: 1 1 150px; display: flex; flex-direction: column; gap: 0.3rem; }

.form-label {
    font-family: var(--font-utility);
    font-size: 0.7rem;
    text-transform: uppercase;
    letter-spacing: 0.06em;
    color: var(--color-rope);
}

.add-quest input, .add-quest select {
    font-family: var(--font-body);
    font-size: 1rem;
    background: transparent;
    border: none;
    border-bottom: 2px solid var(--color-rope);
    padding: 0.35rem 0.1rem;
    color: var(--color-ink);
    outline: none;
    transition: border-color 0.2s ease;
}

.add-quest input:focus, .add-quest select:focus {
    border-bottom-color: var(--color-rust);
}

.add-quest .btn {
    font-family: var(--font-utility);
    border-radius: 3px;
    border: 1px solid var(--color-rope);
    cursor: pointer;
    align-self: center;
    margin-top: 0.5rem;
    padding: 0.65rem 1.6rem;
    font-size: 0.85rem;
    background: linear-gradient(180deg, var(--color-brass-light), var(--color-brass));
}

.btn:hover { transform: translateY(-2px); box-shadow: 0 4px 0 rgba(0,0,0,0.3); }
.btn:active { transform: translateY(0); box-shadow: 0 1px 0 rgba(0,0,0,0.3); }

</style>