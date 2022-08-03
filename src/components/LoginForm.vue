<template>
  <h1>Connexion</h1>

  <form @submit.prevent>
    <label for="email">Your email adress</label>
    <input
      type="text"
      name="email"
      placeholder="Jsmitch@gmail.com"
      v-model="email"
    />
    <label for="password">Create un password</label>
    <input
      type="password"
      name="password"
      placeholder="1234"
      v-model="password"
    />

    <input type="submit" value="Valider" @click="getLogin" />
  </form>
</template>

<script>
export default {
  name: "restaurantForm",
  data() {
    return {
      restorers: [],
      email: "",
      password: "",
    };
  },
  methods: {
    async getLogin() {
      const body = {
        email: this.email,
        password: this.password,
      };

      const response = await fetch("http://127.0.0.1:8000/api/login", {
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

  mounted() {
    this.getLogin();
  },
};
</script>

<style></style>
