<template>
  <div>
    <v-row class="justify-center">
      <v-col cols="12" md="4">
        <v-overlay
          :value="showCardInfo"
          :dark="$vuetify.theme.dark"
          @click="showCardInfo = !showCardInfo"
        >
          <v-card class="mx-auto mw-75" outlined v-show="showCardInfo">
            <v-list-item three-line>
              <v-list-item-content>
                <v-row no-gutters class="justify-space-between">
                  <div class="text-overline mb-4">{{ username }}</div>
                </v-row>

                <v-list-item-title class="text-h5 mb-1">
                  {{ name }}
                </v-list-item-title>
                <v-list-item-subtitle class="d-flex justify-space-between">
                  <span><i>Telefone:</i> {{ phone }}</span>
                  <span><i>Website:</i> {{ website }}</span>
                  <span><i>email:</i> {{ email }}</span>
                </v-list-item-subtitle>
              </v-list-item-content>
            </v-list-item>
            <v-card-text>
              <div class="text--primary">
                <strong>Endereço</strong>
                <v-list-item-subtitle class="d-flex justify-space-between">
                  <span><i>Rua:</i> {{ street }}</span>
                  <span><i>Complemento:</i> {{ suite }}</span>
                  <span><i>Cidade:</i> {{ city }}</span>
                  <span><i>Código Postal:</i> {{ zipcode }}</span>
                </v-list-item-subtitle>
              </div>
              <div class="text--primary">
                <strong>Companhia</strong>
                <v-list-item-subtitle class="d-flex justify-space-between">
                  <span><i>Nome</i> {{ companyname }}</span>
                  <span><i> {{ companyphrase }}</i>
                  </span>
                  <span><i>{{ bs }}</i>
                  </span>
                </v-list-item-subtitle>
              </div>
            </v-card-text>
          </v-card>
        </v-overlay>
      </v-col>
    </v-row>

    <v-item-group>
      <v-container>
        <v-row>
          <v-col cols="12" md="4" v-for="(item, index) in items" :key="item.id">
            <CardUsuario
              v-bind:name="item.name"
              v-bind:username="item.username"
              v-bind:email="item.email"
              v-bind:phone="item.phone"
              v-bind:website="item.website"
              v-bind:index="index"
              @emit-click="getInfo"
            >
            </CardUsuario>
          </v-col>
        </v-row>
      </v-container>
    </v-item-group>
  </div>
</template>

<script>
import CardUsuario from "../components/CardUsuario";
import axios from "axios";
export default {
  name: "Home",

  data() {
    return {
      items: [],
      name: "",
      username: "",
      email: "",
      phone: "",
      website: "",
      index: -1,
      showCardInfo: false,
      street: "",
      suite: "",
      city: "",
      bs: "",
      zipcode: "",
      companyphrase: "",
      companyname: "",
    };
  },
  components: {
    CardUsuario,
  },
  methods: {
    getInfo(index) {
      this.index = index;
      this.name = this.items[index].name;
      this.username = this.items[index].username;
      this.email = this.items[index].email;
      this.phone = this.items[index].phone;
      this.website = this.items[index].website;
      if (!this.showCardInfo) {
        this.showCardInfo = !this.showCardInfo;
      }
      this.street = this.items[index].address.street;
      this.suite = this.items[index].address.suite;
      this.city = this.items[index].address.city;
      this.zipcode = this.items[index].address.zipcode;

      this.bs = this.items[index].company.bs;
      this.companyphrase = this.items[index].company.catchPhrase;
      this.companyname = this.items[index].company.name;
    },
  },

  async created() {
    // GET request using axios with async/await
    const response = await axios.get(
      "https://jsonplaceholder.typicode.com/users"
    );
    this.items = response.data;
    console.log(response.data);
  },
};
</script>
