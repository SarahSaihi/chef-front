<template>
  <h1>Liste de vos restaurants</h1>

  <ul>
    <li v-for="restaurant in restaurants" :key="restaurant.id">
      <p>Nom: <input type="text" v-model="restaurant.namerestaurant" /></p>
      <p>Adresse: <input type="text" v-model="restaurant.adress" /></p>
      <p>Horaires: <input type="text" v-model="restaurant.hours" /></p>
      <p>Image: <input type="text" v-model="restaurant.picture" /></p>
      <button @click="changeRestaurant(restaurant)">MODIFIER</button>
      <button @click="deleteRestaurant(restaurant.id)">SUPPRIMER</button>
    </li>
  </ul>
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
      this.restaurants = data.restaurants;
    },
    async createrestaurant() {
      const body = {
        nameRestorant: this.namerestaurant,
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
    async changeRestaurant(restaurant) {
      const body = restaurant;

      const response = await fetch("http://127.0.0.1:8000/api/restaurant/" + restaurant.id, {
        method: "PUT",
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
  mounted() {
    this.getrestaurants();
  },
};
</script>

<style>
.container-lists-restaurants {
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 135px;
}
.title-lists-restaurants {
  color: white;
}
.box {
  height: 139px;
  width: 354px;
  background: white;
  color: #361b17;
  padding: 20px;
}
h1 {
  text-align: center;
}
li {
  list-style: none;
}
</style>
