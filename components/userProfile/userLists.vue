<template>
  <div class="container">
    <b-card no-body>
      <b-tabs pills card justified>
        <b-tab title="Fav Beers" active>
          <FavBeersArray></FavBeersArray>
        </b-tab>
        <b-tab title="Wished Beers">
          <WishedBeersArray></WishedBeersArray>
        </b-tab>
        <b-tab title="Done Beers">
          <DoneBeersArray></DoneBeersArray>
        </b-tab>
        <b-tab title="Hated Beers">
          <HatedBeersArray></HatedBeersArray>
        </b-tab>
      </b-tabs>
    </b-card>
  </div>
</template>

<script>
import FavBeersArray from '@/components/userProfile/userArrays/FavBeersArray'
import WishedBeersArray from '@/components/userProfile/userArrays/WishedBeersArray'
import DoneBeersArray from '@/components/userProfile/userArrays/DoneBeersArray'
import HatedBeersArray from '@/components/userProfile/userArrays/HatedBeersArray'

export default {
  components: {
    FavBeersArray,
    WishedBeersArray,
    DoneBeersArray,
    HatedBeersArray
  }

};
</script>
