<template>
  <div class="photo__container" v-bind:style="styleContainer" >
    <img class="photo__image" v-bind:src="`${item.url}`">
  </div>
</template>

<script>
  export default {
    name: 'ImageBlock',
    props: {
      item: Object
    },
    data() {
      return {
        width: this.item.width ? this.item.width : 0,
        height: this.item.height ? this.item.height : 0
      }
    },
    async mounted() {
      const root = this;
      let getImage = src => {
        let data = new Image()
        data.src = src;
        data.onload = function() {
          root.width = this.width;
          root.height = this.height;
        };
      }

      if(!this.item.width || !this.item.height) {
        getImage(this.item.url);
      }

    },
    computed: {
      styleContainer() {
        return {'width': this.width*200/this.height + 'px', 'flex-grow': this.width*200/this.height}
      }
    }
  }
</script>