<template>
  <div id="app">
    <h3>Cadastro</h3>

    <form @submit="createUser($event)">
      <input type="text" placeholder="nome" v-model="nameField" />
      <input type="email" placeholder="email" v-model="emailField" />
      <input type="number" placeholder="age" v-model="ageField" />

      <button type="submit">Cadastrar</button>
    </form>

    <h1>Clientes</h1>
    <div v-for="client in orderClients" :key="client.id">
      <Client
        :client="client"
        :showAge="false"
        @deleteClient="deleteClient($event)"
      />
    </div>
    <!-- <Cliente email="gabrieltsunoda@gmail.com" :nome="nomeCliente" idade="55" /> -->
  </div>
</template>

<script>
import _ from "lodash";
import Client from "./components/Client";

export default {
  name: "App",
  data() {
    return {
      nameField: "",
      emailField: "",
      ageField: "",
      clients: [
        {
          id: "1",
          name: "Tsunoda",
          email: "gabrieltsunoda@gmail.com",
          age: 15,
        },
        {
          id: "2",
          name: "A Tsunoda 2 ",
          email: "gabrieltsunoda@gmail.com",
          age: 15,
        },
        {
          id: "3",
          name: "Tsunoda 3",
          email: "gabrieltsunoda@gmail.com",
          age: 15,
        },
      ],
    };
  },
  components: {
    Client,
  },
  methods: {
    createUser: function ($event) {
      $event.preventDefault();

      const client = {
        id: Date.now(),
        name: this.nameField,
        email: this.emailField,
        age: this.ageField,
      };

      this.clients.push(client);
    },
    deleteClient: function ($event) {
      const { id } = $event;

      const updatedClients = this.clients.filter((client) => client.id != id);

      this.clients = updatedClients;
    },
  },
  computed:{
    orderClients: function(){
      return _.orderBy(this.clients, ['name'], ['asc'])
    }
  },
  
};
</script>

<style>
</style>
