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
          <!-- pour l'instant affiche toutes les quêtes, il faudra filtrer en fonction du status de la quête-->
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
      const quests = JSON.parse(savedQuests);
      console.log("Parsed quests: ", quests);
      if (quests.length === 0) {
        quests = [{id: 0, name: "Commencez votre aventure", desc: "Ceci est une quête d'exemple pour démontrer les fonctionnalités de l'application.", difficulty: 3, reward: 100, status: "Disponible", dateLimite: new Date().toISOString().split('T')[0]}];
      }
      return {
        quests: quests
      };
    } else {
      return {
        quests: [{id: 0, name: "Commencez votre aventure", desc: "Ceci est une quête d'exemple pour démontrer les fonctionnalités de l'application.", difficulty: 3, reward: 100, status: "Disponible", dateLimite: new Date().toISOString().split('T')[0]}]
      };
    }
  },
  methods:{
    addQuest(quest) { // quest est un dictionnaire avec les propriétés de la quête
      if (this.quests.length >= 1) {
        quest.id = this.quests[this.quests.length - 1].id + 1;
      }
      this.quests.push(quest);
      localStorage.setItem('quests', JSON.stringify(this.quests));
    },
    deleteCard(id) {
      this.quests = this.quests.filter(quest => quest.id !== id);
      localStorage.setItem('quests', JSON.stringify(this.quests));
    }
  }
}
</script>

<style scoped>
</style>
