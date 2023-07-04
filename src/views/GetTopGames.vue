<template>
<div id="GetTopGamesContainer">
    <topNavBarLinks></topNavBarLinks>
    <h1>List of Top Games</h1>
    <div id="topGames">
        <div class="topGame" v-for='topGame in listOfTopGames'
        :key='topGame.gameID'>
            <div class="topGameThumbnailContainer">
                <img class="topGameThumbnail" :src="`${topGame.gameBoxArtURL}`" alt="">
                <p>{{topGame.gameName}}</p>
            </div>
        </div>
    </div>
</div>    
</template>

<script>
import topNavBarLinks from '../components/topNavBarLinks';

export default{
  name: 'GetTopGames',
  data: function () {
      return{
          listOfTopGames: [],
      }
  },
  components: {
      topNavBarLinks,
  },
  methods: {
      fetchTopGames: function () {
          let fetchLink = 'https://api.twitch.tv/helix/games/top?first=30';

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
                    console.log(data)

                    let dataListOfTopGames = [];

                    for (var key in data.data){
                        dataListOfTopGames.push({
                            gameID: data.data[key].id,
                            gameName: data.data[key].name,
                            gameBoxArtURL: data.data[key].box_art_url.replace('{width}', '213').replace('{height}', '285'),
                        });
                    }

                    this.listOfTopGames = [...this.listOfTopGames, ...dataListOfTopGames]
                }
            )
      }
  },
  mounted () {
      this.fetchTopGames();
  }
}
</script>
<style>
#topGames {
    display: flex;
    flex-wrap: wrap;
}
.topGame{
    flex-basis: 100%;
    padding: 7px;
}
.topGameThumbnail{
    width: 100%;
}

@media only screen and (min-width: 350px){
    .topGame{
        flex-basis: 50%;
    }
}
@media only screen and (min-width: 650px){
    .topGame{
        flex-basis: 33.333333;
    }
}
@media only screen and (min-width: 950px){
    .topGame{
        flex-basis: 25%;
    }
}
@media only screen and (min-width: 1250px){
    .topGame{
        flex-basis: 20%;
    }
}
@media only screen and (min-width: 1550px){
    .topGame{
        flex-basis: 16.66666667%;
    }
}
@media only screen and (min-width: 1550px){
    .topGame{
        flex-basis: 14.28571428571429%;
    }
}
</style>