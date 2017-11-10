
<template>
      <div class="LatestArticles">
          <div class="col-md-4 col-sm-6 col-xs-12 article" v-for="article in newsFeed">
              <a :href="article.Url" :target="article.Target">
                <img :src="article.ThumbnailUrl" class="img-responsive">
                <h4>{{article.Title}}</h4>
              </a>
              <h5>{{article.PublishFromDate | filterDate}}</h5>
              <span style="font-style:italic">{{article.Description}}</span>
          </div>
      </div>
</template>

<script>
import Slick from 'vue-slick';
import axios from 'axios';
export default {
    data() {
        return {
          newsFeed: {}
        };
    },
    mounted() {
      this.getNewsFeedAPI();
    },
    methods: {
        getNewsFeedAPI() {
            var vm = this;
            axios.get(`https://www.ctv.ca/api/curatedfilter/byfilter/3c4d81e6-45f1-4b90-8728-2c93583d6b36/1/8`)
              .then(function(response) {
                  vm.newsFeed = response.data.Items;
              })
              .catch(function (error) {
                  alert("There has been an error!!");
              })
        }
    }
}
</script>

<style type="text/css">

.article {
  padding-bottom:30px;
}

.article {
  min-height: 400px !important;
}

@media (min-width:1025px) {
  .col-md-4:nth-child(3n+3) + .col-md-4{clear:both;}

}
@media (min-width:1281px) {
  .col-md-4:nth-child(3n+3) + .col-md-4{clear:both;}
}

@media only screen and (max-width : 480px) {
  .article {
      min-height:0px;
      padding-bottom:20px;
  }
}
</style>
