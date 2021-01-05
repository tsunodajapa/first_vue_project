<template>
  <div id="cliente-nome" :class="isPremium ? 'client' : 'clientPremium'">
    <h4>Nome: {{ client.name }}</h4>

    <p>Email: {{ client.email | processEmail }}</p>
    <p v-if="showAge">Idade: {{ client.age }}</p>
    <p v-else>Não idade</p>

    <input type="text" v-model="client.name" />

    <button @click="changeColor">Mudar cor</button>
    <button @click="emitEvent">Deletar</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      isPremium: false,
    };
  },
  props: {
    client: {
      id: String,
      name: String,
      email: String,
      age: Number,
    },
    showAge: Boolean,
  },
  methods: {
    changeColor: function () {
      this.isPremium = !this.isPremium;
    },
    emitEvent: function () {
      this.$emit("deleteClient", {id: this.client.id});
    },
  },
  filters:{
    processEmail: function(value){
      return value.toUpperCase();
    }
  },
  computed: {
    SpecialId: function(){
      return (this.client.email);
    }
  }
};
</script>

<style scoped>
.client {
  background: #f10;
}

.clientPremium {
  background: #1f0;
}
</style>