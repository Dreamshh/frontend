<template>
  <section>
    <greeting-card :username="savedUsername" />

    <h2>Здесь вы сможете легко и быстро купить билет на самолет.</h2>
    <v-row>
      <v-col cols="5" class="mx-auto">
        <v-card class="px-10 py-5">
          <v-btn
            color="accent"
            class="mb-3 mr-3"
            @click="$router.push(`/flight/`)"
            >Рейсы</v-btn
          >
          <br />
          <v-btn
            color="accent"
            class="mb-3 mr-3"
            @click="$router.push(`/planes/`)"
            >Наши самолеты</v-btn
          >
          <br />
          <v-btn
            color="accent"
            class="mb-3 mr-3"
            @click="$router.push(`/passengers/`)"
            >Наши пассажиры</v-btn
          >
           <br />
          <v-btn
            color="accent"
            class="mb-3 mr-3"
            @click="$router.push(`/tickets/`)"
            >Купленные билеты</v-btn
          >
           <br />
          <v-btn
            color="accent"
            class="mb-3 mr-3"
            @click="$router.push(`/logout/`)"
            >Выйти</v-btn
          >
        </v-card>
      </v-col>
    </v-row>
  </section>
</template>
 
<script>
import GreetingCard from "@/components/GreetingCard";

export default {
  name: "Greeting",

  components: {
    GreetingCard,
  },

  data: () => ({
    username: "",

    savedUsername: "",
  }),

  methods: {},

  created() {
    // если localStorage содержит значение по ключу
    // username, то запишем его в наши переменные
    if (localStorage.getItem("username")) {
      this.savedUsername = localStorage.getItem("username");

      this.username = this.savedUsername;
    }
  },
};
</script>
 
<style>
.greeting-list-wrapper {
  display: flex;
}

.greeting-list-wrapper .greeting-list {
  margin: auto;
}
</style>

