<template>
  <div>
    <div>
      <b-card no-body>
        <b-card-header header-tag="nav">
          <b-nav card-header pills justified>
            <b-nav-item @click.prevent="showFavs">Fav Beers</b-nav-item>
            <b-nav-item @click.prevent="showHates">Hate Beers</b-nav-item>
            <b-nav-item @click.prevent="showDone">Done Beers</b-nav-item>
            <b-nav-item @click.prevent="showWish">Wish Beers</b-nav-item>
          </b-nav>
        </b-card-header>

        <b-card-body>
          <b-card-title :title="title"> {{this.title}} </b-card-title>

          <b-card-text>
            {{this.user.beers}}
          </b-card-text>
        </b-card-body>
      </b-card>
    </div>
  </div>
</template>

<script>

export default {
  data() {
    return {
      user: {
        title:"",
        beers: [],
      },
    };
  },
  async mounted() {

  },
  methods: {
  async showFavs(){
    let userID = window.localStorage.getItem('id')
    let response = await this.$axios.get(`beers`);
    this.user.beers = response.data
    }
  },
    async showHates(){
    let userID = window.localStorage.getItem('id')
    let response = await this.$axios.get(`beers`);
    this.user.beers = response.data
  },
  showDone(){
    let userID = window.localStorage.getItem('id')
    this.user.beers = JSON.parse(localStorage.getItem("beerDone"))
  },
    showWish(){
    let userID = window.localStorage.getItem('id')
    this.user.beers = JSON.parse(localStorage.getItem("beerWish"))
  }
};
</script>
