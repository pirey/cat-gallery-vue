<template>
  <div class="container">
    <h2 class="my-3">Favorit Saya</h2>
    <div class="row">
      <div :key="favourite.id" v-for="favourite in favourites" class="col-6 col-sm-4 mb-3">
        <button
          @click="removeFavourite(favourite)"
          class="btn btn-block btn-danger"
        >
          Unlike
        </button>
        <img
          class="d-block img-fluid"
          style="max-height: 300px"
          :src="favourite.image.url"
          alt="a cat"
        />
      </div>
    </div>

    <h2 class="my-3">
      Gallery Kucing
      <button @click="getImages()" class="btn btn-secondary">
        Refresh
      </button>
    </h2>
    <div class="row">
      <div :key="image.id" v-for="image in images" class="col-6 col-sm-4 mb-3">
        <button
          @click="addFavourite(image)"
          class="btn btn-block btn-primary"
        >
          Like
        </button>
        <img
          class="d-block img-fluid"
          style="max-height: 300"
          :src="image.url"
          alt="a cat"
        />
      </div>
    </div>
  </div>
</template>

<script>
import catApi from '../cat-api'

export default {
  name: 'Gallery',
  data() {
    return {
      favourites: [],
      images: []
    }
  },
  mounted() {
    this.getImages()
  },
  methods: {
    addFavourite(image) {
      catApi.addFavourite(image.id).then(() => {
        this.getFavourites()
      })
    },
    removeFavourite(favourite) {
      catApi.removeFavourite(favourite.id).then(() => {
        this.getFavourites()
      })
    },
    getFavourites() {
      catApi.getFavourites().then(favourites => {
        this.favourites = favourites
      })
    },
    getImages() {
      catApi.getImages().then(images => {
        this.images = images
      })
    }
  }
}
</script>
