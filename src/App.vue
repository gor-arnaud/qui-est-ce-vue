<template>
  <h1>Qui est-ce ? (un jeu MB®)</h1>
  <div class="board">
    <div class="criteria">
      <h2>Critères</h2>
      <h3 v-if="filteredPersons.length === 1">C'est&nbsp;{{ filteredPersons[0].id }}!!!</h3>
      <h3 v-else>{{ filteredPersons.length }}&nbsp;suspect(s)</h3>
      <div class="criteriaList">
        <div v-for="criterion in criteria" :key="criterion">
          <select v-model="criterion.value">
            <option
              v-for="value in values"
              :key="value.value"
              :value="value.value"
            >
              {{ value.text }}
            </option>
          </select>
          {{ criterion.id }}
        </div>
        <div>
          <button @click="resetCriteria">Réinitialiser</button>
        </div>
      </div>
    </div>
    <div class="grid">
      <PersonCard v-for="person in filteredPersons" :key="person.id" :person="person"></PersonCard>
    </div>
  </div>
</template>

<script>
import persons from "./assets/persons.json";
import PersonCard from "./components/personCard.vue";

export default {
  name: "App",
  components: {
    PersonCard
  },
  data() {
    return {
      persons: persons,
      criteria: [],
      values: [
        { text: "---", value: null },
        { text: "Oui", value: true },
        { text: "Non", value: false },
      ],
    };
  },
  computed: {
    filteredPersons() {
      return persons.filter((person) => {
        for (let i = 0; i < this.criteria.length; i++) {
          const criterion = this.criteria[i];

          if (criterion.value === null) {
            continue;
          }

          if (person[criterion.id] != criterion.value) {
            return false;
          }
        }

        return true;
      });
    },
  },
  methods: {
    resetCriteria() {
      this.criteria.forEach(criterion => {
        criterion.value = null;
      });
    }
  },
  mounted() {
    this.criteria = Object.keys(persons[0])
      .filter((key) => key !== "id")
      .map((key) => {
        return {
          id: key,
          value: null,
        };
      });
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.board {
  display: flex;
  flex-direction: column;
}
.grid {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  border: 1px solid #c1c1c1;
  border-radius: 5px;
  padding: 5px;
  gap: 10px;
}
.criteriaList {
  display: flex;
  flex-direction: column;
}
</style>
