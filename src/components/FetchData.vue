<template>
  <div>
    <h1>Total spent this Month: {{ totalSpent }}</h1>
    <Chart :prices="allPrices" :categories="allCategories" />
  </div>
</template>

<script>
import axios from "axios";
import Chart from "./Chart.vue";
export default {
  name: "FetchData",
  components: {
    Chart,
  },

  mounted() {
    this.fetchData();
  },

  data() {
    return {
      totalSpent: 0,
      allPrices: [],
      allCategories: [],
    };
  },

  methods: {
    fetchData() {
      axios
        .get(
          "https://notion-api.splitbee.io/v1/table/3200aa61a1fd408c927192c1843c337b"
        )
        .then(
          (response) => {
            console.log(response.data);
            let hej = [];
            let categories = [];
            response.data.forEach((element) => {
              console.log(element.Price);
              this.totalSpent = this.totalSpent + element.Price;
              hej.push(element.Price);
              categories.push(element.Category);
              console.log(hej);
              this.allPrices = hej;
              this.allCategories = categories;
            });
          },
          (error) => {
            console.log(error);
          }
        );
    },
  },
};
</script>

<style></style>
