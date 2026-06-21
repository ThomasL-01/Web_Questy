<template>
  <header class="header">
    <h1>Questy</h1>
  </header>

  <Board>
    <table class="board">
      <tbody>
        <tr>
          <td>
            <Column title="Disponibles" class="col-available">
              <Card v-for="quest in quests.filter(q => q.status === 'Disponible')" :key="quest.id"
                :id="quest.id"
                :name="quest.name"
                :desc="quest.desc"
                :difficulty="quest.difficulty"
                :status="quest.status"
                :dateLimite="quest.dateLimite"
                @delete-card="deleteCard"
                @update-status="updateStatus"
                @click="openModal(card)"
              />
            </Column>
          </td>
          <td>
            <Column title="En cours" class="col-progress">
              <Card v-for="quest in quests.filter(q => q.status === 'En cours')" :key="quest.id"
                :id="quest.id"
                :name="quest.name"
                :desc="quest.desc"
                :difficulty="quest.difficulty"
                :status="quest.status"
                :dateLimite="quest.dateLimite"
                @delete-card="deleteCard"
                @update-status="updateStatus"
                @click="openModal(card)"
              />
            </Column>
          </td>
          <td>
            <Column title="Terminées" class="col-done">
              <Card v-for="quest in quests.filter(q => q.status === 'Terminée')" :key="quest.id"
                :id="quest.id"
                :name="quest.name"
                :desc="quest.desc"
                :difficulty="quest.difficulty"
                :status="quest.status"
                :dateLimite="quest.dateLimite"
                @delete-card="deleteCard"
                @click="openModal(card)"
              />
            </Column>
          </td>
          <td>
            <Column title="Échouées" class="col-failed">
              <Card v-for="quest in quests.filter(q => q.status === 'Échouée')" :key="quest.id"
                :id="quest.id"
                :name="quest.name"
                :desc="quest.desc"
                :difficulty="quest.difficulty"
                :status="quest.status"
                :dateLimite="quest.dateLimite"
                @delete-card="deleteCard"
                @click="openModal(card)"
              />
            </Column>
          </td>
        </tr>
      </tbody>
    </table>
  </Board>

  <Form @add-card="(quest) => addQuest(quest)"/>

  <footer>
    <p>Questy par Thomas inspiration Pirate</p>
  </footer>
</template>

<script>
import Card from './Components/Card.vue';
import Column from './Components/Column.vue';
import Board from './Components/Board.vue';
import Form from './Components/Form.vue';

export default {
  components: {
    Card,
    Column,
    Board,  
    Form
  },
  data () {
    const savedQuests = localStorage.getItem('quests'); // On récupère les quêtes sauvegardées dans le localStorage
    if (savedQuests) { // Si des quêtes sont trouvées dans le localStorage, on les charge
      return {
        quests: JSON.parse(savedQuests),
      };
    } else { // Si aucune quête n'est trouvée dans le localStorage, on initialise avec une quête par défaut
      return {
        quests: [{id: 0, name: "Commencez votre aventure", desc: "Ceci est une quête d'exemple.", difficulty: 3, status: "Disponible", dateLimite: new Date().toISOString().split('T')[0]}],
      };
    }
  },
  methods:{
    addQuest(quest) { // quest est un dictionnaire avec les propriétés de la quête recues de Form.vue
      if (quest.name.trim() === '') { // Vérifie si le nom de la quête est vide
        alert("Le nom de la quête ne peut pas être vide.");
        return;
      }
      if (this.quests.length >= 1) { // Vérifie si la liste de quêtes n'est pas vide pour attribuer un nouvel ID
        quest.id = this.quests[this.quests.length - 1].id + 1;
      }
      this.quests.push(quest); // On ajoute la nouvelle quête à la liste et on met à jour le localStorage
      this.checkExpiredQuests(this.quests); // Vérifie les quêtes expirées après l'ajout (vérifie que la date qui vient d'être ajoutée n'est pas déjà expirée)
      localStorage.setItem('quests', JSON.stringify(this.quests));
    },
    deleteCard(id) {
      this.quests = this.quests.filter(quest => quest.id !== id); // On supprime la quête correspondante de la liste et on met à jour le localStorage
      localStorage.setItem('quests', JSON.stringify(this.quests));
    },
    updateStatus(array) {
      const [id, newStatus] = array; // On déstructure le tableau pour obtenir l'id et le nouveau statut
      const quest = this.quests.find(q => q.id === id); // On met à jour le statut de la quête correspondante
      if (quest) { // On vérifie si la quête existe et on met à jour son statut dans le localStorage
        quest.status = newStatus;
        localStorage.setItem('quests', JSON.stringify(this.quests));
      }
    },
    checkExpiredQuests(quests) {
      const today = new Date().toISOString().split('T')[0]; // On récupère la date d'aujourd'hui au format YYYY-MM-DD
      var changed = false;
      quests.forEach(quest => {// On parcourt toutes les quêtes Disponibles et En cours pour vérifier si elles sont expirées
        if ((quest.status === 'Disponible' || quest.status === 'En cours') && quest.dateLimite < today) {
          quest.status = 'Échouée';
          changed = true;
        }
      });
      if (changed) { // Si au moins une quête a été modifiée, on met à jour le localStorage
        localStorage.setItem('quests', JSON.stringify(quests));
      }
    }
  }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Pirata+One&family=IM+Fell+English:ital@0;1&family=Cinzel:wght@500;600&display=swap');

:root {
  --color-ocean-deep: #0a2530;
  --color-ocean-mid: #123b48;
  --color-ocean-light: #1f5563;
  --color-parchment: #ecdfb4;
  --color-parchment-dark: #d8c08a;
  --color-parchment-shadow: #b89a5e;
  --color-brass: #c9974c;
  --color-brass-light: #e3b96b;
  --color-ink: #2b1c10;
  --color-rope: #6b4423;
  --color-rust: #8a3324;
  --color-rust-dark: #5e2015;
  --color-emerald: #2f6b4f;
  --color-emerald-dark: #1d4632;

  --font-display: 'Pirata One', serif;
  --font-body: 'IM Fell English', Georgia, serif;
  --font-utility: 'Cinzel', serif;
}

* { box-sizing: border-box; }

body {
  margin: 0;
  min-height: 100vh;
  font-family: var(--font-body);
  color: var(--color-parchment);
  background:
    radial-gradient(ellipse at 20% -10%, rgba(255,255,255,0.05), transparent 40%),
    radial-gradient(ellipse at 80% 110%, rgba(255,255,255,0.04), transparent 45%),
    repeating-linear-gradient(0deg, rgba(255,255,255,0.015) 0px, rgba(255,255,255,0.015) 1px, transparent 1px, transparent 3px),
    linear-gradient(160deg, var(--color-ocean-deep) 0%, var(--color-ocean-mid) 55%, var(--color-ocean-deep) 100%);
  background-attachment: fixed;
}

a:focus-visible, button:focus-visible, input:focus-visible, select:focus-visible {
  outline: 2px solid var(--color-brass-light);
  outline-offset: 2px;
}

@media (prefers-reduced-motion: reduce) {
  * { transition: none !important; animation: none !important; }
}
</style>

<style scoped>
.header {
  text-align: center;
  padding: 2.5rem 1rem 1.5rem;
}

.header h1 {
  display: inline-block;
  margin: 0;
  font-family: var(--font-display);
  font-size: clamp(2.5rem, 6vw, 4rem);
  letter-spacing: 0.08em;
  color: var(--color-brass-light);
  text-shadow:
    0 1px 0 #000,
    0 3px 6px rgba(0,0,0,0.6),
    0 0 30px rgba(201,151,76,0.25);
}

.header h1::before,
.header h1::after {
  content: '☠';
  font-family: var(--font-utility);
  font-size: 0.5em;
  color: var(--color-brass);
  vertical-align: middle;
  margin: 0 0.6em;
  opacity: 0.8;
}

.board {
  width: 100%;
  border-collapse: separate;
  border-spacing: 1.25rem;
  table-layout: fixed;
  margin: 0;
}

.board td {
  vertical-align: top;
  width: 25%;
}

footer {
  text-align: center;
  padding: 2rem 1rem 3rem;
  font-family: var(--font-utility);
  font-size: 0.75rem;
  letter-spacing: 0.04em;
  color: rgba(236,223,180,0.45);
}

@media (max-width: 800px) {
  .board, .board tbody, .board tr, .board td {
    display: block;
    width: 100%;
  }
  .board { border-spacing: 0; }
  .board td { margin-bottom: 1.25rem; }
}
</style>