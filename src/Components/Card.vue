<template>
    <div class="card" :data-status="status">
        <div class="card__seal">
            <p v-if="difficulty == 1" class = "easy">⭐</p>
            <p v-if="difficulty == 2" class = "easy">⭐ ⭐</p>
            <p v-if="difficulty == 3" class = "medium">⭐ ⭐ ⭐</p>
            <p v-if="difficulty == 4" class = "hard">⭐ ⭐ ⭐ ⭐</p>
            <p v-if="difficulty == 5"class = "hard">⭐ ⭐ ⭐ ⭐ ⭐</p>
        </div>
        <h3 class="card__title">{{ name }}</h3>
        <p class="card__desc">{{ desc }}</p>
        <div class="card__meta">
            <p> Date limite : {{ dateLimite }}</p>
        </div>
        <div class="card__actions">
            <button v-if="status== 'Disponible'" class="btn btn--accept" @click="$emit('update-status', [id, 'En cours'])">Passer en cours</button>
            <button v-if="status == 'En cours'" class="btn btn--complete" @click="$emit('update-status', [id, 'Terminée'])">Passer en terminée</button>
            <label v-if="status == 'Échouée'" class="echouee">Quete Echouée !</label>
            <button class="btn btn--delete" @click="$emit('delete-card', id)">Supprimer</button>
        </div>
    </div>
</template>
<script>
export default { 
    emits: ['delete-card', 'update-status'],   // 2 événements émis : suppression de la carte et mise à jour du statut
    props: { // 7 propriétés reçues du parent (App.vue)
        id : Number,
        name : String,
        desc : String,
        difficulty : Number,
        status : String,
        dateLimite : String
    },
};
</script>
<style scoped>
.card {
    position: relative;
    background:
        repeating-linear-gradient(0deg, rgba(0,0,0,0.02) 0 2px, transparent 2px 4px),
        radial-gradient(circle at 30% 20%, rgba(139,94,38,0.15), transparent 60%),
        var(--color-parchment);
    color: var(--color-ink);
    font-family: var(--font-body);
    padding: 1.5rem 1.1rem 1rem;
    border-radius: 2px;
    box-shadow:
        0 1px 0 rgba(255,255,255,0.4) inset,
        0 8px 16px rgba(0,0,0,0.4),
        0 2px 0 var(--color-parchment-shadow);
    transform: rotate(-1deg);
    transition: transform 0.25s ease, box-shadow 0.25s ease;
    clip-path: polygon(0% 2%, 3% 0%, 97% 1%, 100% 3%, 99% 97%, 96% 100%, 2% 99%, 1% 96%);
}

.card:nth-child(even) { transform: rotate(1.2deg); }
.card:nth-child(3n)   { transform: rotate(-0.6deg); }

.card:hover {
    transform: rotate(0deg) translateY(-4px) scale(1.015);
    box-shadow: 0 14px 26px rgba(0,0,0,0.5), 0 2px 0 var(--color-parchment-shadow);
}

.card::after {
    content: '';
    position: absolute;
    top: -10px;
    left: 50%;
    transform: translateX(-50%);
    width: 16px;
    height: 16px;
    border-radius: 50%;
    background: radial-gradient(circle at 35% 30%, #d8d8d8, #8a8a8a 70%, #5a5a5a);
    box-shadow: 0 2px 3px rgba(0,0,0,0.5);
}

.card[data-status="Échouée"] { box-shadow: 0 0 0 2px var(--color-rust) inset, 0 8px 16px rgba(0,0,0,0.4); }
.card[data-status="Terminée"] { box-shadow: 0 0 0 2px var(--color-emerald) inset, 0 8px 16px rgba(0,0,0,0.4); }

.card__seal {
    position: absolute;
    top: -16px;
    right: -10px;
    width: 58px;
    height: 58px;
    border-radius: 50%;
    background: radial-gradient(circle at 35% 30%, var(--color-brass-light), var(--color-brass) 60%, #8a6324 100%);
    border: 2px solid #5e431c;
    box-shadow: 0 3px 6px rgba(0,0,0,0.5);
    display: flex;
    align-items: center;
    justify-content: center;
    transform: rotate(8deg);
    padding: 4px;
}

.card__seal p {
    margin: 0;
    font-size: 0.5rem;
    line-height: 1.15;
    text-align: center;
    letter-spacing: -1px;
    text-shadow: 0 1px 0 rgba(255,255,255,0.3);
}

.card__seal .easy   { color: #1f4a36; }
.card__seal .medium { color: #5c360c; }
.card__seal .hard   { color: #5c150c; }

.card__title {
    font-family: var(--font-display);
    font-size: 1.3rem;
    margin: 0 0 0.35rem;
    color: var(--color-rust-dark);
    letter-spacing: 0.02em;
}

.card__desc {
    font-style: italic;
    font-size: 0.92rem;
    line-height: 1.4;
    margin: 0 0 0.75rem;
    color: rgba(43,28,16,0.85);
}

.card__meta {
    display: flex;
    justify-content: space-between;
    gap: 0.5rem;
    font-family: var(--font-utility);
    font-size: 0.68rem;
    text-transform: uppercase;
    letter-spacing: 0.03em;
    color: var(--color-rope);
    border-top: 1px dashed rgba(107,68,35,0.4);
    padding-top: 0.5rem;
    margin: 0 0 0.75rem;
}
.card__meta p { margin: 0; }

.card__actions {
    display: flex;
    flex-wrap: wrap;
    gap: 0.5rem;
}

.btn {
    font-family: var(--font-utility);
    font-size: 0.7rem;
    text-transform: uppercase;
    letter-spacing: 0.05em;
    padding: 0.5rem 0.8rem;
    border-radius: 3px;
    border: 1px solid var(--color-rope);
    cursor: pointer;
    background: linear-gradient(180deg, #efe2c0, #d8c08a);
    color: var(--color-ink);
    box-shadow: 0 2px 0 rgba(0,0,0,0.25);
    transition: transform 0.15s ease, box-shadow 0.15s ease;
}

.btn:hover { transform: translateY(-2px); box-shadow: 0 4px 0 rgba(0,0,0,0.3); }
.btn:active { transform: translateY(0); box-shadow: 0 1px 0 rgba(0,0,0,0.3); }

.btn--accept   { background: linear-gradient(180deg, var(--color-brass-light), var(--color-brass)); }
.btn--complete { background: linear-gradient(180deg, #5fae8a, var(--color-emerald)); color: #f3efe0; }
.btn--delete   { background: linear-gradient(180deg, #b85b48, var(--color-rust)); color: #f3efe0; border-color: var(--color-rust-dark); }

.echouee {
    font-family: var(--font-utility);
    font-size: 0.7rem;
    text-transform: uppercase;
    letter-spacing: 0.05em;
    padding: 0.5rem 0.8rem;
    border-radius: 3px;
    border: 1px solid var(--color-rope);
    cursor: pointer;
    color: var(--color-ink);
    box-shadow: 0 2px 0 rgba(0,0,0,0.25);
    transition: transform 0.15s ease, box-shadow 0.15s ease;
}
</style>