<template>
  <v-card class="mx-auto" max-width="344" outlined elevation="8">
    <v-list-item three-line>
      <v-list-item-content>
        <div class="text-overline mb-4">{{ username }}</div>
        <v-list-item-title class="text-h5 mb-1"> {{ name }}</v-list-item-title>
        <v-list-item-subtitle> </v-list-item-subtitle>
      </v-list-item-content>
    </v-list-item>

    <v-card-actions> 
      <v-btn outlined rounded text @click="showContact"> Contact </v-btn>
      <v-btn outlined rounded text @click="showInfo(index)"> Info </v-btn>
    </v-card-actions>
    <v-scroll-y-transition>
      <div v-if="active" class="flex-grow-1">
        <v-card-text>
          <div class="text--primary">
            <p><i>Telefone:</i> {{ phone }}</p>
            <p><i>Website:</i> {{ website }}</p>
          </div>
        </v-card-text>
      </div>
    </v-scroll-y-transition>
  </v-card>
</template>

<script>
export default {
  name: "CardUsuario",
  data() {
    return {
      active: false,
    };
  },
  props: ["name", "username", "email", "phone", "website", "index"],
  methods: {
    showContact() {
      this.active = !this.active;
    },
    showInfo(index){
       this.$emit('emit-click', index);
    },
  },
};
</script>
