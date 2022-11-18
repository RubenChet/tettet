<template>
  <div>
    <div class="grid_container">
      <!-- <h1 >Message: {{ items.ID }}</h1> -->
      <vs-row>
        <vs-card
          v-for="items in myData"
          type="2"
          v-bind:key="items.ID"
          v-on:click="ChangePage(items)"
        >
          <template #title> </template>
          <template #text> </template>
          <template #img>
            <div class="in_card">
              <p class="inner-txt">{{ items.Domaine }}</p>
            </div>
          </template>
        </vs-card>
      </vs-row>
    </div>
  </div>
</template>

<script>
import domaines_file from "../domaine.json";
import json_file from "../GR491.json";
export default {
  data: () => ({
    myData: domaines_file,
  }),
  methods: {
    ChangePage: function (domaine) {
      this.$root.$emit("Home.ChangePage", domaine);
    },
  },
  created() {
    let jsonData = json_file.filter((e) => e["incontournables"] == "INCONTOURNABLE");
    for (let item of jsonData) {
      this.$cart.push(item);
    }
  },
};
</script>

<style>
.grid_container {
  display: flex;
  justify-content: center;
}
.vs-row {
  display: flex;
  justify-content: space-around !important;
  max-width: 80%;
}
.vs-card {
  border-radius: 10px !important;
  margin-top: 10px;
}
.in_card {
  width: 350px;
  height: 200px;
  display: flex;
  justify-content: center;
  align-items: center;
}
.border {
  border: 3px solid black;
}
.inner-txt{
  font-size: 1.5em;
  max-width: 80%;
  text-align: center;
}
li {
  display: flex;
  justify-content: center;
}
.vs-pagination-content {
  margin-top: 30px;
}
</style>
