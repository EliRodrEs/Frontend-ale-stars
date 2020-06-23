<template>
  <div class="allTheBeers">
    <!--    <beerFilters></beerFilters> -->
    <div class="container">
      <div class="row">
        <ul class="b-table">
          <li v-for="beer in beers" :key="beer.id" class="col">
            <b-card :title="beer.name" :sub-title="beer.brewery" class="own-card">
              <b-card-text>
                <ul class="list">
                  <li>{{ beer.type }}</li>
                  <li>||</li>
                  <li>{{ beer.style }}</li>
                  <li>||</li>
                  <li>{{ beer.grad }}</li>
                  <li>||</li>
                  <li>{{ beer.country }}</li>
                </ul>
              </b-card-text>
              <b-card-text class="beer-desc">{{beer.description}}</b-card-text>
              <b-card-text>
                <ul class="list">
                  <li>
                    <b-button @click.prevent="checkDoneList(beer)">
                      <fa icon="thumbtack" :color="variantDone(beer)" />
                    </b-button>
                  </li>
                  <li>||</li>
                  <li>
                    <b-button @click.prevent="checkHateList(beer)">
                      <fa icon="hand-middle-finger" :color="variantHate(beer)" />
                    </b-button>
                  </li>
                  <li>||</li>
                  <li>
                    <b-button @click.prevent="checkWishList(beer)">
                      <fa icon="list" :color="variantWish(beer)" />
                    </b-button>
                  </li>
                  <li>||</li>
                  <li>
                    <b-button @click.prevent="checkFavList(beer)">
                      <fa icon="star" class="disable" :color="variantFav(beer)" />
                    </b-button>
                    {{beer.favRating}}
                  </li>
                </ul>
              </b-card-text>
              <!--                 <a href="#" class="card-link">HOLA LINK AQUÍ</a> -->
            </b-card>
          </li>
        </ul>
      </div>
    </div>
  </div>
</template>

<script>
import beerFilters from "@/components/beerFilters.vue";
import Swal from "sweetalert2";

export default {
  props: ["beers"],
  data() {
    return {
      favBeers: null,
      hatedBeers: null,
      wishedBeers: null,
      doneBeers: null
    };
  },
  mounted() {
    this.loadMarkedBeers();
  },
  components: {
    beerFilters
  },
  methods: {
    loadMarkedBeers() {
      this.favBeers = JSON.parse(localStorage.getItem("beerFav"));
      this.hatedBeers = JSON.parse(localStorage.getItem("beerHate"));
      this.wishedBeers = JSON.parse(localStorage.getItem("beerWish"));
      this.doneBeers = JSON.parse(localStorage.getItem("beerDone"));
    },
    variantFav(beer) {
      if (!this.favBeers) return "#35383F";
      let foundBeer = this.favBeers.some(b => b === beer._id);
      if (!foundBeer) {
        return "#35383F";
      } else {
        return "#D5D9BA";
      }
    },
    variantHate(beer) {
      if (!this.hatedBeers) return "#35383F";
      let foundBeer = this.hatedBeers.some(b => b === beer._id);
      if (!foundBeer) {
        return "#35383F";
      } else {
        return "#D5D9BA";
      }
    },
    variantWish(beer) {
      if (!this.wishedBeers) return "#35383F";
      let foundBeer = this.wishedBeers.some(b => b === beer._id);
      if (!foundBeer) {
        return "#35383F";
      } else {
        return "#D5D9BA";
      }
    },
    variantDone(beer) {
      if (!this.doneBeers) return "#35383F";
      let foundBeer = this.doneBeers.some(b => b === beer._id);
      if (!foundBeer) {
        return "#35383F";
      } else {
        return "#D5D9BA";
      }
    },
    async checkFavList(beer) {
      try {
        let favBeers = JSON.parse(localStorage.getItem("beerFav"));
        let foundBeer = favBeers.some(b => b === beer._id);
        if (!foundBeer) {
          this.addFav(beer);
          favBeers.push(beer._id);
          this.favBeers = favBeers.slice();
          this.addFavBeer(beer);
          window.localStorage.setItem("beerFav", JSON.stringify(favBeers));
        } else {
          this.removeFav(beer);
          const index = favBeers.indexOf(beer._id);
          favBeers.splice(index, 1);
          this.favBeers = favBeers.slice();
          this.removeFavBeer(beer);
          window.localStorage.setItem("beerFav", JSON.stringify(favBeers));
        }
      } catch (error) {
        Swal.fire({
          icon: "error",
          title: "Go home, you are drunk",
          text: "You are not even logged in, mate",
          footer: "<a href=/login>Where should I start?</a>",
          confirmButtonColor: "#FC9935",
          buttons: {
            confirm: { text: "OK", className: "sweet-ok" }
          }
        });
      }
    },
    async addFav(beer) {
      let token = localStorage.getItem("token");
      const response = await this.$axios.put(`beers/${beer._id}/favs`, null, {
        headers: {
          Authorization: `Bearer ${token}`
        }
      });
    },
    async removeFav(beer) {
      let token = localStorage.getItem("token");
      const response = await this.$axios.patch(`beers/${beer._id}/favs`, null, {
        headers: {
          Authorization: `Bearer ${token}`
        }
      });
    },
    async addFavBeer(beer) {
      let token = localStorage.getItem("token");
      const userID = window.localStorage.getItem("id");
      const response = await this.$axios.patch(`users/${userID}/favs`, null, {
        params: { fav: beer._id },
        headers: {
          Authorization: `Bearer ${token}`
        }
      });
    },
    async removeFavBeer(beer) {
      let token = localStorage.getItem("token");
      const userID = window.localStorage.getItem("id");
      const response = await this.$axios.patch(`users/${userID}/favs`, null, {
        params: { unfav: beer._id },
        headers: {
          Authorization: `Bearer ${token}`
        }
      });
    },

    async checkHateList(beer) {
      try {
        let hateBeers = JSON.parse(localStorage.getItem("beerHate"));
        let foundBeer = hateBeers.some(b => b === beer._id);
        if (!foundBeer) {
          hateBeers.push(beer._id);
          this.hatedBeers = hateBeers.slice();
          this.addHateBeer(beer);
          window.localStorage.setItem("beerHate", JSON.stringify(hateBeers));
        } else {
          const index = hateBeers.indexOf(beer._id);
          hateBeers.splice(index, 1);
          this.hatedBeers = hatedBeers.slice();
          this.removeHateBeer(beer);
          window.localStorage.setItem("beerHate", JSON.stringify(hateBeers));
        }
      } catch (error) {
        Swal.fire({
          icon: "error",
          title: "Go home, you are drunk",
          text: "You are not even logged in, mate",
          footer: "<a href=/login>Where should I start?</a>",
          confirmButtonColor: "#FC9935"
        });
      }
    },
    async addHateBeer(beer) {
      let token = localStorage.getItem("token");
      const userID = window.localStorage.getItem("id");
      const response = await this.$axios.patch(`users/${userID}/hates`, null, {
        params: { hate: beer._id },
        headers: {
          Authorization: `Bearer ${token}`
        }
      });
    },
    async removeHateBeer(beer) {
      let token = localStorage.getItem("token");
      const userID = window.localStorage.getItem("id");
      const response = await this.$axios.patch(`users/${userID}/hates`, null, {
        params: { unhate: beer._id },
        headers: {
          Authorization: `Bearer ${token}`
        }
      });
    },

    async checkWishList(beer) {
      try {
        let wishBeers = JSON.parse(localStorage.getItem("beerWish"));
        let foundBeer = wishBeers.some(b => b === beer._id);
        if (!foundBeer) {
          wishBeers.push(beer._id);
          this.wishedBeers = wishBeers.slice();
          this.addWishBeer(beer);
          window.localStorage.setItem("beerWish", JSON.stringify(wishBeers));
        } else {
          const index = wishBeers.indexOf(beer._id);
          wishBeers.splice(index, 1);
          this.wishedBeers = wishedBeers.slice();
          this.removeWishBeer(beer);
          window.localStorage.setItem("beerWish", JSON.stringify(wishBeers));
        }
      } catch (error) {
        Swal.fire({
          icon: "error",
          title: "Go home, you are drunk",
          text: "You are not even logged in, mate",
          footer: "<a href=/login>Where should I start?</a>",
          confirmButtonColor: "#FC9935",
          buttons: {
            confirm: { text: "OK", className: "sweet-ok" }
          }
        });
      }
    },
    async addWishBeer(beer) {
      const userID = window.localStorage.getItem("id");
      const response = await this.$axios.patch(`users/${userID}/wish`, null, {
        params: { wish: beer._id }
      });
    },
    async removeWishBeer(beer) {
      const userID = window.localStorage.getItem("id");
      const response = await this.$axios.patch(`users/${userID}/wish`, null, {
        params: { unwish: beer._id }
      });
    },
    async checkDoneList(beer) {
      try {
        let doneBeers = JSON.parse(localStorage.getItem("beerDone"));
        let foundBeer = doneBeers.some(b => b === beer._id);
        if (!foundBeer) {
          doneBeers.push(beer._id);
          this.doneBeers = doneBeers.slice();
          this.addDoneBeer(beer);
          window.localStorage.setItem("beerDone", JSON.stringify(doneBeers));
        } else {
          const index = doneBeers.indexOf(beer._id);
          doneBeers.splice(index, 1);
          this.doneBeers = doneBeers.slice();
          this.removeDoneBeer(beer);
          window.localStorage.setItem("beerDone", JSON.stringify(doneBeers));
        }
      } catch (error) {
        Swal.fire({
          icon: "error",
          title: "Go home, you are drunk",
          text: "You are not even logged in, mate",
          footer: "<a href=/login>Where should I start?</a>",
          confirmButtonColor: "#FC9935",
          buttons: {
            confirm: { text: "OK", className: "sweet-ok" }
          }
        });
      }
    },
    async addDoneBeer(beer) {
      const userID = window.localStorage.getItem("id");
      const response = await this.$axios.patch(`users/${userID}/done`, null, {
        params: { done: beer._id }
      });
    },
    async removeDoneBeer(beer) {
      const userID = window.localStorage.getItem("id");
      const response = await this.$axios.patch(`users/${userID}/done`, null, {
        params: { undone: beer._id }
      });
    }
  }
};
</script>



