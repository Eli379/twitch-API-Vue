<template>
<div id="topStreamersContainer">
    <topNavBarLinks></topNavBarLinks>
    <h1>List of Top Streamers</h1>
</div>    
</template>

<script>
import topNavBarLinks from '../components/topNavBarLinks';

export default{
  name: 'GetTopGames',
  data: function (){
      return{
          listOfTopGames: [],

      }
  },
  components: {
      topNavBarLinks,
  },
  methods: {
      fetchTopStreamers: function () {
          let fetchLink = 'https://api.twitch.tv/kraken/streams/summary?game=Overwatch';

          fetch(fetchLink, {
              method: 'get',
              headers: new Headers({
                  'Authorization': 'Bearer xthxexqknseetme08puw0yx4ksmecd',
                  'Client-ID': 'gwxcieyri7n0r4kj6x4h5je8rs9pv0'
              })
          })
            .then(
                function (response) {
                    return response.json();
                }
            )
            .then(
                data => {
                    console.log(data);
                }
            )
      }
  },
  mounted () {
      this.fetchTopStreamers();
  }
}
</script>
<style>

</style>