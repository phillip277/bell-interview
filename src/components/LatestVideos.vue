
<template>
  <div class="LatestVideos">
      <carousel :perPage="4" :navigationEnabled="true" :paginationEnabled="false" :perPageCustom="[[300, 1], [1200, 4], [600, 2], [768, 2], [1024, 4]]">
          <slide v-for="item in videoFeed" class="container-image" :key="item.Id">
              <span v-for="image in item.Images">
                  <img :src="image.Url" v-if="image.Type =='thumbnail'" class="video-thumbnail img-responsive">
              </span>
              <div class="play">
                  <img src="../assets/play.svg" class="play-button">
              </div>
              <div class="overlay">
                 <span class="text">{{item.Name}}</span>
                 <span class="text-right text-right-season">S{{item.Season.Number}} E{{item.Episode}}</span>
              </div>
          </slide>
     </carousel>
  </div>
</template>

<script>
import Slick from 'vue-slick';
import axios from 'axios';
import { Carousel, Slide } from 'vue-carousel';
export default {
    components: { Carousel, Slide },
    data() {
        return {
          options: {
              perPage: 4,
          },
          videoFeed: {}
        };
    },
    mounted() {
      this.getVideoFeedAPI();
    },
    methods: {
        getVideoFeedAPI() {
            var vm = this;
            axios.get(`https://capi.9c9media.com/destinations/ctv_web/platforms/desktop/collections/88/contents?$include=[Episode,Media.Id,Season,ItemsType,Items.ID,Images,Type,ShortDesc,Media.Name,Season,Episode,Genres]&$inlinecount=true&$page=1&$top=7&type=episode`)
              .then(function(response) {
                  vm.videoFeed = response.data.Items;
              })
              .catch(function (error) {
                  alert("There has been an error!!");
              })
        }
    }
}
</script>

<style type="text/css">

.container-image {
  position:relative;
  display:inline-block;
  overflow:hidden;
  transition: 0.5s all;
}

.container-image:last-child {
  width:10px;
}
.container-image:first-child {
  margin-left: 10px;
  margin-right: 10px;
}
.VueCarousel-navigation--disabled[data-v-7fed18e9] {
    color: grey !important;
}
.VueCarousel-navigation-prev {
  background: rgba(0, 0, 0, 0.3);
  color: yellow !important;
}
.VueCarousel-navigation-button:hover {
   color: blue !important;
}
.VueCarousel-navigation--disabled[data-v-7fed18e9]:hover {
    color: grey !important;
}
.VueCarousel-navigation-next {
  background: rgba(0, 0, 0, 0.3);
  color: yellow !important;
}
.play-button {
  width: 40px;
  height: 40px;
  position: absolute;
  top: 9px;
  left: 10px;
}
.text-right-season {
  padding: 8px 10px 10px 10px !important;
  color:#fff;
  right:0;
  float:right;
  font-size: 12px;
}
.video-thumbnail {
  width:250px;
}
.container-image:hover {
  transform:scale(1.5);
  -ms-transform:scale(1.5);
  -moz-transform:scale(1.5);
  -webkit-transform:scale(1.04);
  -o-transform:scale(1.1);
}

.overlay {
  position: absolute;
  bottom: 0;
  left: 0;
  right: 0;
  height: 30%;
  max-height: 35%;
  width:250px;
  transition: .5s ease;
  background-color: rgba(0, 0, 0, 0.5);
}
.text {
  width:80%;
  display:block;
  color: white;
  font-size: 12px;
  position: absolute;
  padding: 7px 4px 5px 10px;
}
.text-right {
    padding: 7px 4px 5px 10px;
}

.VueCarousel-navigation--disabled .VueCarousel-navigation-next {
  background-color: rgba(0, 0, 0, 0.3);
}
/* Extra Small Devices, Phones */
@media only screen and (max-width : 480px) {
  .video-thumbnail {
    display: block;
    max-width: 100%;
    max-height: 100%;
    width: 100%;
    height: 100%;
  }
  .container-image:first-child {
    margin-left:auto;
    margin-right: auto;
  }

  .overlay {
    position: absolute;
    bottom: 0;
    left: 0;
    right: 0;
    height: 30%;
    width: 100%;
    transition: .5s ease;
    background-color: rgba(0, 0, 0, 0.5);
  }

  .text {
    width:80%;
    display:block;
    color: white;
    font-size: 12px;
    position: absolute;
    padding: 7px 4px 5px 10px;
  }
  .VueCarousel-navigation-next[data-v-7fed18e9] {
    right:1px;
  }
}
</style>
