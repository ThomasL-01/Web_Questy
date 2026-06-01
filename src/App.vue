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
          <Column title="Disponible"> 
            <Card v-for="quest in quests" :key="quest.id"
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
            <Card v-for="quest in quests" :key="quest.id" 
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
          <Column title="Terminée">
            <Card v-for="quest in quests" :key="quest.id"
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
          <Column title="Échouée">
            <Card v-for="quest in quests" :key="quest.id"
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

    <Form @add-card="addQuest"/>

    <div class = "footer">
      <p>© 2026 Questy. Tous droits réservés. (askip)</p>
    </div>
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
        quests: JSON.parse(savedQuests)
      };
    } else {
      return {
        quests: []
      };
    }
  },
  methods:{
    addQuest(quest) {
      this.quests.push(quest);
      localStorage.setItem('quests', JSON.stringify(this.quests));
    },
  }
}
</script>

<style scoped>
</style>
