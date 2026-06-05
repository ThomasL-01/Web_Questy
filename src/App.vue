<template>
  <header>
    <title>Questy - Page principale</title>
  </header>
  <body>
    <div class="header">
      <h1>Questy</h1>
    </div>

    <Board>
      <table>
        <td>
          <Column title="Disponibles"> 
            <Card v-for="quest in quests.filter(q => q.status === 'Disponible')" :key="quest.id"
              :id="quest.id"
              :name="quest.name"
              :desc="quest.desc"
              :difficulty="quest.difficulty"
              :status="quest.status"
              :reward="quest.reward"
              :dateLimite="quest.dateLimite"
              @delete-card="deleteCard"
              @update-status="updateStatus"
              @click="openModal(card)"
            />
          </Column>
        </td>
        <td>
          <Column title="En cours">
            <Card v-for="quest in quests.filter(q => q.status === 'En cours')" :key="quest.id"
              :id="quest.id"
              :name="quest.name"
              :desc="quest.desc"
              :difficulty="quest.difficulty"
              :status="quest.status"
              :reward="quest.reward"
              :dateLimite="quest.dateLimite"
              @delete-card="deleteCard"
              @update-status="updateStatus"
              @click="openModal(card)"
            />
          </Column>
        </td>
        <td>
          <Column title="Terminées">
            <Card v-for="quest in quests.filter(q => q.status === 'Terminée')" :key="quest.id"
              :id="quest.id"
              :name="quest.name"
              :desc="quest.desc"
              :difficulty="quest.difficulty"
              :status="quest.status"
              :reward="quest.reward"
              :dateLimite="quest.dateLimite"
              @delete-card="deleteCard"
              @click="openModal(card)"
            />
          </Column>
        </td>
        <td>
          <Column title="Échouées">
            <Card v-for="quest in quests.filter(q => q.status === 'Échouée')" :key="quest.id"
              :id="quest.id"
              :name="quest.name"
              :desc="quest.desc"
              :difficulty="quest.difficulty"
              :status="quest.status"
              :reward="quest.reward"
              :dateLimite="quest.dateLimite"
              @delete-card="deleteCard"
              @click="openModal(card)"
            />
          </Column>
        </td>
      </table>
    </Board>

    <Form @add-card="(quest) => addQuest(quest)"/>

    <footer>
      <p>© 2026 Questy. Tous droits réservés. (askip)</p>
    </footer>
  </body>

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
    const savedQuests = localStorage.getItem('quests');
    if (savedQuests) {
      return {
        quests: JSON.parse(savedQuests),
        modalOpen: false, form: {}
      };
    } else {
      return {
        quests: [{id: 0, name: "Commencez votre aventure", desc: "Ceci est une quête d'exemple.", difficulty: 3, reward: 100, status: "Disponible", dateLimite: new Date().toISOString().split('T')[0]}],
        modalOpen: false, form: {}
      };
    }
  },
  methods:{
    addQuest(quest) { // quest est un dictionnaire avec les propriétés de la quête
      if (quest.name.trim() === '') {
        alert("Le nom de la quête ne peut pas être vide.");
        return;
      }
      if (this.quests.length >= 1) {
        quest.id = this.quests[this.quests.length - 1].id + 1;
      }
      this.quests.push(quest);
      localStorage.setItem('quests', JSON.stringify(this.quests));
    },
    deleteCard(id) {
      this.quests = this.quests.filter(quest => quest.id !== id);
      localStorage.setItem('quests', JSON.stringify(this.quests));
    },
    updateStatus(array) {
      const [id, newStatus] = array;
      const quest = this.quests.find(q => q.id === id);
      if (quest) {
        quest.status = newStatus;
        localStorage.setItem('quests', JSON.stringify(this.quests));
      }
    }
  }
}
</script>

<style>
</style>
