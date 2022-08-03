<template>
  <h1>Inscription</h1>

  <form @submit.prevent="createRestorer">
    <label for="firstname">Your firstname</label>
    <input
      type="text"
      name="firstname"
      placeholder="John"
      v-model="firstname"
    />
    <label for="lastname">Your name</label>
    <input type="text" name="lastname" placeholder="Smith" v-model="lastname" />

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

    <input type="submit" value="Valider" @click="getRestorers" />
  </form>
</template>

<script>
export default {
  name: "InscriptionForm",
  data() {
    return {
      restorers: [],
      firstname: "",
      lastname: "",
      email: "",
      password: "",
    };
  },
  methods: {
    async getRestorers() {
      const response = await fetch("http://127.0.0.1:8000/api/inscription", {
        method: "GET",
        headers: {
          Accept: "application/json",
        },
      });

      const data = await response.json();
      console.log(data);
    },

    async createRestorer() {
      const body = {
        firstname: this.firstname,
        lastname: this.lastname,
        email: this.email,
        password: this.password,
      };

      const response = await fetch("http://127.0.0.1:8000/api/inscription", {
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
    this.getRestorers();
  },
};
</script>

<style></style>
