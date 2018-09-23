<template>
  <div>
  <div id='gallery'>
    <div class="masonry masonry--h">
      <figure v-for="image in images" class="masonry-brick masonry-brick--h">
        <img :src="image.urls.regular" class="masonry-img" @click="openImageEditor(image)">
      </figure>
    </div>
  </div>
  <ImageEditor v-if="currentImage" :image="currentImage"/>
  </div>
</template>

<script>
import axios from 'axios';
import ImageEditor from './ImageEditor.vue';

const API_END_POINT = 'https://api.unsplash.com';
const API_ACCESS_KEY = '027fbdbaa9b670f0009962019861081abff81fec413a30c5f90aa7c591343ef5';

export default {
  components: {
    ImageEditor
  },
  props: {
  },
  data: function() {
    return {
      images: [],
      currentImage: null
    }
  },
  created: function(){
    this.fetchImages();
  },
  mounted: function(){
    this.hideModalListener();
  },
  methods: {
    fetchImages: function(){
      let self = this;

      axios.get(`${API_END_POINT}/photos?client_id=${API_ACCESS_KEY}&per_page=50`)
        .then(function(response){
          self.images = response.data;
        })
    },
    openImageEditor: function(image) {
      this.currentImage = image;
    },
    hideModalListener: function() {
      let self = this;
      document.onclick = function(e){
        if(e.target.className == 'modal'){
          self.currentImage = null;
        }
      };
    }
  }
}
</script>

<style scoped>
.masonry {
  display: flex;
  width: 100%;
}

.masonry--h {
  flex-flow: row wrap;
}

.masonry--v {
  flex-flow: column wrap;
  max-height: 1080px;
}

.masonry--h, .masonry--v {
  margin-left: -8px; /* Adjustment for the gutter */
  counter-reset: brick;
}

.masonry-brick {
  overflow: hidden;
  border-radius: 5px;
  margin: 0 0 8px 8px;  /* Some Gutter */
  background-color: #333;
  color: white;
  position: relative;
}

.masonry-brick:hover:after {
  font-size: 2.25em;
  opacity: 1;
}

.masonry-brick--h {
  flex: auto;
  height: 250px;
  min-width: 150px;
}

@media only screen and (min-width: 1024px) {
  /* Horizontal masonry bricks on desktop-sized screen */
  .masonry-brick--h:nth-child(4n+1) {
    width: 250px;
  }
  .masonry-brick--h:nth-child(4n+2) {
    width: 325px;
  }
  .masonry-brick--h:nth-child(4n+3) {
    width: 180px;
  }
  .masonry-brick--h:nth-child(4n+4) {
    width: 380px;
  }

  /* Adjusting vertical masonry height on desktop-sized screen */
  .masonry--v {
    max-height: 1600px;
  }

  /* Vertical masonry bricks on desktop-sized screen */
  .masonry-brick--v {
    width: 33.33333%;
  }
}

@media only screen and (max-width: 1023px) and (min-width: 768px) {
  /* Horizontal masonry bricks on tabled-sized screen */
  .masonry-brick--h:nth-child(4n+1) {
    width: 200px;
  }
  .masonry-brick--h:nth-child(4n+2) {
    width: 250px;
  }
  .masonry-brick--h:nth-child(4n+3) {
    width: 120px;
  }
  .masonry-brick--h:nth-child(4n+4) {
    width: 280px;
  }

  /* Adjusting vertical masonry height on tablet-sized screen */
  .masonry--v {
    max-height: 2000px;
  }

  /* Vertical masonry bricks on tablet-sized screen */
  .masonry-brick--v {
    width: 50%;
  }
}

.masonry-img {
  object-fit: cover;
  width: 100%;
  height: 100%;
}

</style>
