
<template>
  <div id="app">
    <div class="container">
        <div class="col-md-12">
          <h2>Latest Episodes</h2>
          <LatestVideos />
        </div>

        <div class="col-md-12">
          <h2>Latest Articles</h2>
        </div>
        <LatestArticles />
    </div>
  </div>
</template>

<script>
import LatestVideos from './components/LatestVideos'
import LatestArticles from './components/LatestArticles'

export default {
  name: 'app',
  components: {
    LatestVideos, LatestArticles
  }
}
</script>
