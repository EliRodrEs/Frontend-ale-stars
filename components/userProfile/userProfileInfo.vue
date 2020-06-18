<template>
  <div>
    <b-card no-body class="overflow-hidden own-card-profile" style="max-width: 540px;">
      <b-row no-gutters>
       <!--  <b-col md="6">
          <b-card-img src="https://picsum.photos/400/200/?image=20" alt="Image" class="rounded-0"></b-card-img>
        </b-col> -->
        <b-col md="6">
          <b-card-body >
            <b-card-text>
              <p class="text-center">BEerHOLD YOUR BEERS!!</p>
            </b-card-text>
          </b-card-body>
        </b-col>
      </b-row>
    </b-card>
  </div>
</template>

<script>

export default {
  data() {
    return {
      user: {
        id: "",
        name: "",
        email: "",
      },
    };
  },
  mounted() {
    this.id = localStorage.getItem("id")
    this.name = localStorage.getItem("name")
    this.email = localStorage.getItem("email")
  },
};
</script>
