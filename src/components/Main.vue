<template>
  <div class="main">
    <vs-navbar
      color="#696969"
      text-white
      square
      center-collapsed
      v-model="active_domain"
    >
      <template #left></template>
      <vs-navbar-item
        v-for="(items, idx) in dfile"
        v-bind:key="idx"
        :active="active_domain == items"
        :id="items"
        v-on:click="GridCreate(items.Code)"
      >
        {{ items.Domaine }}
      </vs-navbar-item>
      <template #right
        ><span @click="active_cart = !active_cart"
          >{{ CartLength()
          }}<i class="pi pi-shopping-cart" @click="DomainValues()"></i></span
      ></template>
    </vs-navbar>
    <div class="the_cart">
      <vs-dialog blur width="800px" not-center v-model="active_cart">
        <div class="car-title">
          <h4 class="not-margin">
            Vous avez {{ cart_length }} Bonnes Pratiques dans votre Panier !
          </h4>
          <vs-button danger @click="allCheck = true"> Finaliser </vs-button>
        </div>

        <template>
          <div class="center">
            <vs-table>
              <template #thead>
                <vs-tr>
                  <vs-th> Domaine </vs-th>
                  <vs-th> Nombre </vs-th>
                </vs-tr>
              </template>
              <template #tbody>
                <vs-tr
                  v-for="(tr, i) in dfile"
                  v-bind:key="i"
                  @click="
                    (active_domain_cart = true),
                      (cart_domain_click = content[i]),
                      (thedomain = tr.Domaine)
                  "
                >
                  <vs-td>
                    {{ tr.Domaine }}
                  </vs-td>
                  <vs-td> {{ content[i].length }} </vs-td>
                  <!-- <template #expand>
                    <div class="con-content">
                      <div
                        v-for="(item, idx) in content[i]"
                        :key="idx"
                        class="cart-sub"
                      >
                        <div class="cart_tab_list">
                          <p>{{ content[i][idx].ID }}</p>
                          <vs-button
                            danger
                            @click="
                              remove_from_cart(content[i][idx]),
                                DomainValues(),
                                refresh_cart()
                            "
                          >
                            <i class="pi pi-times-circle"></i>
                          </vs-button>
                        </div>
                      </div>
                    </div>
                  </template> -->
                </vs-tr>
              </template>
            </vs-table>
          </div>
        </template>
      </vs-dialog>
    </div>
    <div class="cart_domain">
      <vs-dialog blur width="1000px" v-model="active_domain_cart">
        <div class="content-center">
          <h4>{{thedomain}}</h4>
          <div class="table">
            <div
              v-for="(item, idx) in cart_domain_click"
              v-bind:key="idx"
              class="table-content"
            >
              <span>{{ item.ID }}</span>
              <span>{{ item[["Planet"]] }}</span>
              <span>{{ item[["Planet"]] }}</span>
              <span>{{ item[["Planet"]] }}</span>
              <vs-button
                class="suppr"
                danger
                @click="
                  remove_from_cart(cart_domain_click[idx]), DomainValues(), active_domain_cart = false
                "
              >
                <i class="pi pi-times-circle"></i>
              </vs-button>
            </div>
          </div>
        </div>
      </vs-dialog>
    </div>
    <div class="popup">
      <vs-dialog blur width="1000px" not-center v-model="active_card">
        <div class="con-content">
          <div class="left-pop">
            <div class="p-titre">
              <span class="pill">{{ card_data["Planet"] }}</span>
              <span class="pill">{{ card_data["People"] }}</span>
              <span class="pill">{{ card_data["prosperity"] }}</span>
            </div>
            <div class="p-titre">
              {{
                card_data[
                  "CRITERES = Plutôt InterrogatifUne recommandation pour N critères"
                ]
              }}
            </div>
            <div class="bordt"></div>
            <div class="l-note">
              <div>
                <span>Difficulté</span>
                <span>{{
                  card_data[
                    "Difficulté de mise en oeuvreSans Objet (N/A)Nombre d'étoiles 1 à 3De simple = *A complexe = ***"
                  ]
                }}</span>
              </div>
              <div>
                <span>Priorité</span>
                <span>{{ card_data["Priorité"] }}</span>
              </div>
              <div>
                <span>Récurrence</span>
                <span>{{ card_data["Récurrence"] }}</span>
              </div>
            </div>
          </div>
          <div class="right-pop">
            <div class="p-titre">
              <h4>Test:</h4>
              <p>
                {{
                  card_data[
                    "TEST 1.1.1test lié au critère, forme interrogative"
                  ]
                }}
              </p>
            </div>
            <div class="p-titre">
              <h4>Précisions:</h4>
              <p>
                {{
                  card_data[
                    "JUSTIFICATIONSQuels sont les arguments factuels qui jusfient que cet éléments soient présent"
                  ]
                }}
              </p>
            </div>
            <div class="p-titre">
              <h4>Use-Case:</h4>
              <p>{{ card_data["Use Case"] }}</p>
            </div>
          </div>
        </div>
      </vs-dialog>
    </div>
    <div class="export">
      <vs-dialog blur width="1000px" not-center v-model="allCheck">
        <h4 class="not-margin">
          Le ficher va être sauvegardé en XLS (Ouvrable sur EXCEL) il ce peut
          qu'une erreur aparaisse à l'ouverture, ingnorez la !
        </h4>
        <vs-button danger @click="exportFile()"> Exporter </vs-button>
      </vs-dialog>
    </div>
    <div class="grid_container">
      <vs-row>
        <vs-card
          v-for="(items, idx) in myData[chunk_num]"
          type="2"
          v-bind:key="idx"
        >
          <template #img>
            <div
              class="car_container"
              @click="(active_card = !active_card), (card_data = items)"
            >
              <div class="score">
                <div class="score_contain">
                  <span class="pill">{{ items["Planet"] }}</span>
                  <span class="pill">{{ items["People"] }}</span>
                  <span class="pill">{{ items["prosperity"] }}</span>
                </div>
              </div>
              <div class="in_card">
                {{
                  items[
                    "CRITERES = Plutôt InterrogatifUne recommandation pour N critères"
                  ]
                }}
              </div>
            </div>
          </template>
          <template #interactions>
            <div v-if="items['incontournables'] == 'INCONTOURNABLE'">
              Incontournable
            </div>
            <div v-else>
              <div v-if="verif_cart(items) == -1">
                <vs-button
                  @click="
                    add_to_cart(items), GridRefresh(items['Famille Origine'])
                  "
                >
                  <i class="pi pi-cart-plus"></i>
                </vs-button>
              </div>
              <div v-else>
                <vs-button
                  danger
                  @click="
                    remove_from_cart(items),
                      GridRefresh(items['Famille Origine'])
                  "
                >
                  <i class="pi pi-times-circle"></i>
                </vs-button>
              </div>
            </div>
          </template>
        </vs-card>
      </vs-row>
    </div>
    <div class="Pagination">
      <div v-for="(num, idx) in this.myData.length" v-bind:key="idx">
        <vs-button
          flat
          :active="active_num == num"
          @click="(active_num = num), ChgPage(idx)"
        >
          {{ num }}
        </vs-button>
      </div>
    </div>
  </div>
</template>

<script>
import json_file from "../GR491.json";
import domaines_file from "../domaine.json";
import _ from "lodash";
import exportFromJSON from "export-from-json";

export default {
  props: ["WhichDomaine"],

  data: () => ({
    myData: "",
    chunk_num: 0,
    dfile: domaines_file,
    active_domain: [],
    active_num: 1,
    number: 1,
    active_card: false,
    active_cart: false,
    active_domain_cart: false,
    card_data: [],
    content: [],
    counter: 0,
    counter2: 0,
    cart_length: 0,
    domain_count: [],
    isShow: true,
    list: [],
    card_pop: [],
    cart_domain_click: [],
    thedomain: "",

    editActive: false,
    edit: null,
    editProp: "",
    m: "",
    allCheck: false,
    page: 1,
    max: 3,
    active: 0,
    selected: [],
  }),
  methods: {
    GridCreate(val) {
      let myData = json_file.filter((e) => e["Famille Origine"] === val);
      myData = myData.filter(
        (e) =>
          e[
            "CRITERES = Plutôt InterrogatifUne recommandation pour N critères"
          ] !== ""
      );
      const chunk = _.chunk(myData, 12);
      this.myData = chunk;
      this.chunk_num = 0;
      this.active_num = 1;
    },
    GridRefresh(val) {
      let myData = json_file.filter((e) => e["Famille Origine"] === val);
      myData = myData.filter(
        (e) =>
          e[
            "CRITERES = Plutôt InterrogatifUne recommandation pour N critères"
          ] !== ""
      );
      const chunk = _.chunk(myData, 12);
      this.myData = chunk;
    },
    ChgPage(n) {
      this.chunk_num = n;
    },
    add_to_cart(val) {
      this.$cart.push(val);
    },
    remove_from_cart(val) {
      this.$cart.splice(this.$cart.indexOf(val), 1);
    },
    verif_cart(val) {
      return this.$cart.indexOf(val);
    },
    CartLength() {
      return this.$cart.length;
    },
    DomainCount(val) {
      if (this.counter2 < this.dfile.length) {
        let DomainNum = this.$cart.filter((e) => e["Famille Origine"] === val);
        return DomainNum.length;
      } else {
        return "";
      }
    },
    DomainValues() {
      this.counter = 0;
      this.content = [];
      this.cart_length = this.$cart.length;
      for (let item of this.dfile) {
        let DomainVal = this.$cart.filter(
          (e) => e["Famille Origine"] === item.Code
        );
        this.content.push(DomainVal);
      }
    },
    test(val) {
      if (this.counter < this.$cart.length) {
        this.counter++;
        return val.ID;
      } else {
        return "";
      }
    },
    exportFile() {
      let data = this.$cart;
      const fileName = "monFichier";
      const exportType = "xls"; //exported type could be text, json, csv, xls, xml
      exportFromJSON({ data, fileName, exportType });
    },
    refresh_cart() {
      active_cart = false;
      sleep(10000);
      active_cart = true;
    },
    sleep(ms) {
      return new Promise((resolve) => setTimeout(resolve, ms));
    },
    teste(val) {
      console.log(typeof val);
      console.log(val);
    },
    pushlist(i, idx) {
      this.list.push[i][idx](this.content[i][idx].ID);
      return this.list[i][idx];
    },
  },
  created() {
    this.active_domain = this.WhichDomaine;
    let myData = json_file.filter(
      (e) => e["Famille Origine"] === this.active_domain.Code
    );
    myData = myData.filter(
      (e) =>
        e[
          "CRITERES = Plutôt InterrogatifUne recommandation pour N critères"
        ] !== ""
    );
    const chunk = _.chunk(myData, 12);
    this.myData = chunk;
  },
  mounted() {
    this.DomainValues();
  },
};
</script>

<style>
.grid_container {
  display: flex;
  justify-content: center;
}
.car-title {
  display: flex;
  justify-content: space-around;
}

.vs-row {
  display: flex;
  justify-content: space-around !important;
  max-width: 80%;
}

.vs-card {
  border-radius: 10px !important;
  margin-top: 10px;
}

.car_container {
  width: 3250px;
  height: 160px;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}
.score {
  display: flex;
  justify-content: flex-start;
  align-items: center;
  width: 80%;
}
.score_contain {
  margin-top: 5px;
}
.con-content {
  display: flex;
  justify-content: space-around;
}
.left-pop {
  width: 100%;
  display: flex;
  flex-direction: column;
  justify-content: space-around;
}
.right-pop {
  width: 100%;
  display: flex;
  flex-direction: column;
  justify-content: center;
  border-left: 2px solid black;
}
.p-titre {
  text-align: center;
}

.in_card {
  font-size: 0.8em;
  max-width: 80%;
  margin-top: -15px;
  text-align: center;
}
.pill {
  background-color: red;
  border: none;
  color: white;
  padding: 2px 5px;
  text-align: center;
  text-decoration: none;
  display: inline-block;
  margin: 4px;
  cursor: pointer;
  border-radius: 16px;
}
.bordt {
  border-top: 2px solid black;
  width: 100%;
}
li {
  display: flex;
  justify-content: center;
}

.Pagination {
  margin-top: 10px;
  display: flex;
  justify-content: center;
}

.cart_tab_list {
  display: flex;
  justify-content: space-space-around;
}

.l-note {
  display: flex;
  justify-content: space-around;
}
.l-note > div {
  display: flex;
  flex-direction: column;
  text-align: center;
}
.p-titre > h4 {
  justify-content: flex-start;
}
.p-titre > p {
  justify-content: center;
  text-align: center;
}
.table {
  width: 80%;
  display: flex;
  flex-direction: column;
  align-items: center;
}
.head {
  display: flex;
  justify-content: space-around;
  width: 100%;
}

.content-center {
  display: flex;
  flex-direction: column;
  align-items: center;
  text-align: center;
}
.table_domain {
  display: flex;
  justify-content: space-around;
  width: 100%;
}
.table-content {
  display: flex;
  justify-content: space-around;
  width: 100%;
}
</style>
