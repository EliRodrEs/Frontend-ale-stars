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
                      <fa icon="thumbtack" />
                    </b-button>
                  </li>
                  <li>||</li>
                  <li>
                    <b-button @click.prevent="checkHateList(beer)">
                      <fa icon="hand-middle-finger" />
                    </b-button>
                  </li>
                  <li>||</li>
                  <li>
                    <b-button @click.prevent="checkWishList(beer)">
                      <fa icon="list" />
                    </b-button>
                  </li>
                  <li>||</li>
                  <li>
                    <b-button @click.prevent="checkFavList(beer)">
                      <fa icon="star" class="disable"/>
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
import Swal from 'sweetalert2'

export default {
  props: ["beers"],
  components: {
    beerFilters
  },
  methods: {
    async checkFavList(beer) {
      try {
        let favBeers = JSON.parse(localStorage.getItem("beerFav"));
        let foundBeer = favBeers.some(b => b._id === beer._id);

        if (!foundBeer) {
          this.addFav(beer);
          favBeers.push(beer);
          this.addFavBeer(beer);
          window.localStorage.setItem("beerFav", JSON.stringify(favBeers));
        } else {
          this.removeFav(beer);
          const index = favBeers.indexOf(beer);
          favBeers.splice(index, 1);
          this.removeFavBeer(beer);
          window.localStorage.setItem("beerFav", JSON.stringify(favBeers));
        }
      } catch (error) {
        Swal.fire({
          icon: 'error',
          title: 'Go home, you are drunk',
          text: 'You are not even logged in, mate',
          footer: '<a href=/login>Where should I start?</a>',
          confirmButtonColor: "#FC9935",
          buttons: {
            confirm : {text:'OK',className:'sweet-ok'},
          },
        })
      }
    },
    async addFav(beer) {
      const response = await this.$axios.put(`beers/${beer._id}/favs`);
    },
    async removeFav(beer) {
      const response = await this.$axios.patch(`beers/${beer._id}/favs`);
    },
    async addFavBeer(beer) {
      const userID = window.localStorage.getItem("id");
      const response = await this.$axios.patch(`users/${userID}/favs`, null, {
        params: { fav: beer._id }
      });
    },
    async removeFavBeer(beer) {
      const userID = window.localStorage.getItem("id");
      const response = await this.$axios.patch(`users/${userID}/favs`, null, {
        params: { unfav: beer._id }
      });
    },

    async checkHateList(beer) {
      try {
        let hateBeers = JSON.parse(localStorage.getItem("beerHate"));
        let foundBeer = hateBeers.some(b => b._id === beer._id);
        if (!foundBeer) {
          hateBeers.push(beer);
          this.addHateBeer(beer);
          window.localStorage.setItem("beerHate", JSON.stringify(hateBeers));
        } else {
          const index = hateBeers.indexOf(beer);
          hateBeers.splice(index, 1);
          this.removeHateBeer(beer);
          window.localStorage.setItem("beerHate", JSON.stringify(hateBeers));
        }
      } catch (error) {
        Swal.fire({
          icon: 'error',
          title: 'Go home, you are drunk',
          text: 'You are not even logged in, mate',
          footer: '<a href=/login>Where should I start?</a>',
          confirmButtonColor: "#FC9935",
          buttons: {
            confirm : {text:'OK',className:'sweet-ok'},
          },
        })
      }
    },
    async addHateBeer(beer) {
      const userID = window.localStorage.getItem("id");
      const response = await this.$axios.patch(`users/${userID}/hates`, null, {
        params: { hate: beer._id }
      });
    },
    async removeHateBeer(beer) {
      const userID = window.localStorage.getItem("id");
      const response = await this.$axios.patch(`users/${userID}/hates`, null, {
        params: { unhate: beer._id }
      });
    },

    async checkWishList(beer) {
      try {
        let wishBeers = JSON.parse(localStorage.getItem("beerWish"));
        let foundBeer = wishBeers.some(b => b._id === beer._id);
        if (!foundBeer) {
          wishBeers.push(beer);
          this.addWishBeer(beer);
          window.localStorage.setItem("beerWish", JSON.stringify(wishBeers));
        } else {
          const index = wishBeers.indexOf(beer);
          wishBeers.splice(index, 1);
          this.removeWishBeer(beer);
          window.localStorage.setItem("beerWish", JSON.stringify(wishBeers));
        }
      } catch (error) {
          Swal.fire({
          icon: 'error',
          title: 'Go home, you are drunk',
          text: 'You are not even logged in, mate',
          footer: '<a href=/login>Where should I start?</a>',
          confirmButtonColor: "#FC9935",
          buttons: {
            confirm : {text:'OK',className:'sweet-ok'},
          },
        })
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
        let foundBeer = doneBeers.some(b => b._id === beer._id);
        if (!foundBeer) {
          doneBeers.push(beer);
          this.addDoneBeer(beer);
          window.localStorage.setItem("beerDone", JSON.stringify(doneBeers));
        } else {
          const index = doneBeers.indexOf(beer);
          doneBeers.splice(index, 1);
          this.removeDoneBeer(beer);
          window.localStorage.setItem("beerDone", JSON.stringify(doneBeers));
      }
      } catch (error) {
        Swal.fire({
          icon: 'error',
          title: 'Go home, you are drunk',
          text: 'You are not even logged in, mate',
          footer: '<a href=/login>Where should I start?</a>',
          confirmButtonColor: "#FC9935",
          buttons: {
            confirm : {text:'OK',className:'sweet-ok'},
          },
        })
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



