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
              <v-list-item-avatar tile size="120" color="transparent">
                <img src="@/assets/ICON.png" alt="" />
              </v-list-item-avatar>
              <v-list-item-content class="ml-5 mt-5 aling-self:start">
                <v-list-item-subtitle class="d-flex justify-space-between">
                  <div class="text-overline">{{ username }}</div>
                </v-list-item-subtitle>
                <v-list-item-title class="text-h5 pb-5">
                  {{ name }}
                </v-list-item-title>
              </v-list-item-content>

              <v-list-item-content class="ml-5 mt-5">
                <v-list-item-subtitle class="d-flex justify-space-between">
                  <v-col no-gutters>
                    <v-row>
                      <p><i>Telefone:</i> {{ phone }}</p>
                    </v-row>
                    <v-row>
                      <p>
                        <i>Website:</i>
                        <a v-bind:href="website">{{ website }}</a>
                      </p>
                    </v-row>
                    <v-row>
                      <p><i>email:</i> {{ email }}</p>
                    </v-row>
                  </v-col>
                </v-list-item-subtitle>
              </v-list-item-content>
            </v-list-item>
            <v-card-text>
              <v-row>
                <v-col class="ml-5">
                  <div class="text--primary">
                    <strong>Endereço</strong>
                    <v-col>
                      <v-row>
                        <span><i>Rua:</i> {{ street }}</span>
                      </v-row>
                      <v-row>
                        <span><i>Complemento:</i> {{ suite }}</span>
                      </v-row>
                      <v-row>
                        <span><i>Cidade:</i> {{ city }}</span>
                      </v-row>
                      <v-row>
                        <span><i>Código Postal:</i> {{ zipcode }}</span>
                      </v-row>
                    </v-col>
                  </div>
                </v-col>
                <v-col>
                  <div class="text--primary">
                    <strong>Companhia</strong>
                    <v-col>
                      <v-row>
                        <span>{{ companyname }}</span>
                      </v-row>
                      <v-row>
                        <span
                          ><i> {{ companyphrase }}</i></span
                        >
                      </v-row>
                      <v-row>
                        <span
                          ><i>{{ bs }}</i></span
                        >
                      </v-row>
                    </v-col>
                  </div>
                </v-col>
              </v-row>
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
