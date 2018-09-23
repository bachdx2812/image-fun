<template>
  <div class="modal">
    <div class="modal-content">
      <figure v-bind:class="customStyle">
        <img :src="image.urls.regular" class="main-img">
      </figure>
      <div class="flex-container">
        <figure :class="style.name" v-for="style in styles" @click="filterImage(style)">
          <img :src="image.urls.thumb">
        </figure>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  components: {
  },
  props: {
    image: {
      type: Object,
      required: true
    }
  },
  data: function(){
    return {
      customStyle: "normal",
    }
  },
  created: function(){
    this.styles = [
      { name: "normal" },
      { name: "clarendon" },
      { name: "gingham" },
      { name: "moon" },
      { name: "lark" },
      { name: "reyes" },
      { name: "juno" },
      { name: "slumber" },
      { name: "aden" },
      { name: "perpetua" },
      { name: "mayfair" },
      { name: "rise" },
      { name: "hudson" },
      { name: "valencia" },
      { name: "xpro2" },
      { name: "willow" },
      { name: "lofi" },
      { name: "inkwell" },
      { name: "nashville" }
    ]
  },
  mounted: function(){
  },
  methods: {
    filterImage: function(style){
      this.customStyle = style.name;
    },
  }
}
</script>

<style>
.modal {
    display: block; /* Hidden by default */
    position: fixed; /* Stay in place */
    z-index: 1; /* Sit on top */
    left: 0;
    top: 0;
    width: 100%; /* Full width */
    height: 100%; /* Full height */
    overflow: auto; /* Enable scroll if needed */
    background-color: rgb(0,0,0); /* Fallback color */
    background-color: rgba(0,0,0,0.4); /* Black w/ opacity */
}

/* Modal Content/Box */
.modal-content {
    background-color: #fefefe;
    margin: 5% auto; /* 15% from the top and centered */
    padding: 20px;
    border: 1px solid #888;
    width: 80%; /* Could be more or less, depending on screen size */
}

/* The Close Button */
.close {
    color: #aaa;
    float: right;
    font-size: 28px;
    font-weight: bold;
}

.close:hover,
.close:focus {
    color: black;
    text-decoration: none;
    cursor: pointer;
}

.main-img {
  width: 100%;
  height: auto;
}

.flex-container {
  display: flex;
  flex-wrap: nowrap;
  overflow-x: auto;
}

.flex-container figure {
  margin: auto;
  flex: 0 0 auto;
}

.flex-container::-webkit-scrollbar-track
{
	-webkit-box-shadow: inset 0 0 6px rgba(0,0,0,0.3);
	border-radius: 10px;
	background-color: #F5F5F5;
}

.flex-container::-webkit-scrollbar
{
  width: 5px;
  background-color: #F5F5F5;
}

.flex-container::-webkit-scrollbar-thumb
{
  border-radius: 10px;
  -webkit-box-shadow: inset 0 0 6px rgba(0,0,0,.3);
  background-color: #555;
}

figure img {
  width: 100%;
}
</style>
