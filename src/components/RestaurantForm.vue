<template>
  <h1>Création restaurant</h1>

  <form @submit.prevent="createrestaurant">
    <label for="namerestaurant">Nom</label>
    <input
      type="text"
      name="namerestaurant"
      placeholder="Indiquez le nom de votre restaurant"
      v-model="namerestaurant"
      @input="changeRestaurant"
    />
    <label for="adress">Adresse</label>
    <input
      type="text"
      name="adress"
      placeholder="Indiquez l'adresse complète"
      v-model="adress"
    />
    <label for="hours">Horaires</label>
    <input
      type="text"
      name="hours"
      placeholder="Indiquez les horaires d'ouvertures et de fermetures"
      v-model="hours"
    />
    <label for="picture">Photo</label>
    <input type="text" name="picture" v-model="picture" />

    <input type="submit" value="Je valide" @click="getrestaurants" />
  </form>
</template>

<script>
export default {
  name: "restaurantForm",
  data() {
    return {
      restaurants: [],
      namerestaurant: "",
      adress: "",
      hours: "",
      picture: "",
    };
  },
  methods: {
    async getrestaurants() {
      const response = await fetch("http://127.0.0.1:8000/api/restaurant", {
        method: "GET",
        headers: {
          Accept: "application/json",
        },
      });

      const data = await response.json();
      this.restorers = data.restorers;
    },

    async createrestaurant() {
      const body = {
        namerestaurant: this.namerestaurant,
        adress: this.adress,
        hours: this.hours,
        picture: this.picture,
      };

      const response = await fetch("http://127.0.0.1:8000/api/restaurant", {
        method: "POST",
        headers: {
          "Content-Type": "application/json",
          Accept: "application/json",
        },
        body: JSON.stringify(body),
      });
      const data = await response.json();

      console.log(data);
    },
  },

  changeRestaurant(e) {
    this.namerestaurant = e.target.value;
  },
  mounted() {
    this.getrestaurants();
  },
};
</script>

<style></style>
