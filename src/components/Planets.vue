<template>
  <div>
    <table>
      <my-select v-model="selectedSort" :options="sortOptions" />
      <thead>
        <tr>
          <th>Name</th>
          <th>Diameter</th>
          <th>Climate</th>
          <th>Population</th>
          <th>Orbital Period</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(planet, idx) in sortedPlanets" :key="idx">
          <td>
            {{ planet.name }}
          </td>
          <td>
            {{ planet.diameter }}
          </td>
          <td>
            {{ planet.climate }}
          </td>
          <td>
            <span v-if="planet.population > 1000000">
              {{ planet.population / 100000 }}kkk
            </span>
            <span v-else-if="planet.population > 10000">
              {{ planet.population / 10000 }}kk
            </span>
            <span v-else-if="planet.population == 'unknown'"> Unknown </span>
            <span v-else> {{ planet.population }}</span>
          </td>
          <td>
            {{ planet.orbital_period }}
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
import useSortedPlanets from "@/hooks/useSortedPlanets";
export default {
  data() {
    return {
      sortOptions: [
        { value: "diameter", name: "Sort by diameter" },
        { value: "orbital_period", name: "Sort by orbital period" },
      ],
    };
  },
  props: {
    planets: {
      type: Array,
      required: true,
    },
  },
  setup(props) {
    const { selectedSort, sortedPlanets } = useSortedPlanets(props.planets);
    return {
      useSortedPlanets,
      selectedSort,
      sortedPlanets,
    };
  },
};
</script>

<style scoped>
table {
  margin-left: auto;
  margin-right: auto;
  border: 2px solid rgb(0, 85, 85);
  border-radius: 3px;
  background-color: #fff;
}

th {
  background-color: rgb(0, 85, 85);
  color: rgba(255, 255, 255, 0.66);
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}

td {
  background-color: #f9f9f9;
}

th,
td {
  min-width: 120px;
  padding: 10px 20px;
}
</style>
