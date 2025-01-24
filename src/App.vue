<template>
  <div class="board">
    <div class="criteria">
      <h2>Critères</h2>
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
      </div>
    </div>
    <div class="grid">
      <div v-for="person in filteredPersons" :key="person.id">
        <img :src="require(`./assets/${person.id}.jpg`)" />
      </div>
    </div>
  </div>
</template>

<script>
import persons from "./assets/persons.json";

export default {
  name: "App",
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
      return persons.filter((p) => {
        for (let i = 0; i < this.criteria.length; i++) {
          const criterion = this.criteria[i];

          if (criterion.value === null) {
            continue;
          }

          console.log("comparaison pour", p, criterion);

          if (p[criterion.id] != criterion.value) {
            return false;
          }
        }

        return true;
      });
    },
  },
  components: {},
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
  display: grid;
  grid-gap: 10px;
  grid-template-columns: 1fr 1fr 1fr;
  grid-auto-columns: 1fr;
  border: 1px solid #c1c1c1;
  border-radius: 5px;
  padding: 5px;
}
.criteriaList {
  display: flex;
  flex-direction: column;
}
</style>
