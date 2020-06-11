<template>
  <div class="allTheBeers">
    <div class="container">
      <div class="row">
<!--           <ul class="b-table">
            <li v-for="beer in beers" :key=beer.id class="col">
              <h1 class="b-name row">{{ beer.name }}</h1>
              <ul class="data-box row">
                <li class="b-data col">{{ beer.country}}</li>
                <li class="b-data col">{{ beer.brewery}}</li>
                <li class="b-data col">{{ beer.type}}</li>
                <li class="b-data col">{{ beer.style}}</li>
                <li class="b-data col">{{ beer.grad}}%</li>
              </ul>
              <p class="b-desc row">{{ beer.description }}</p>
            </li>
          </ul> -->

          <ul class="b-table">
            <li v-for="beer in beers" :key=beer.id class="col">
              <b-card :title="beer.name" :sub-title="beer.brewery" class="beer-card">
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
                    <li><a><fa icon="thumbtack"/></a></li>
                    <li>||</li>
                    <li><a><fa icon="hand-middle-finger"/></a></li>
                    <li>||</li>
                    <li><a><fa icon="list"/></a></li>
                    <li>||</li>
                    <li><a><fa icon="star"/></a></li>
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
export default {
  data() {
    return {
      beers: [],
    };
  },
  async mounted() {
    let response = await this.$axios.get("/beers");
    this.beers = response.data;
  },
};
</script>




