<template>
  <div id="app">
    <div class="top">
      <InputForm @clear="clear" @get="get" @load="load"/>
    </div>
    <div class="photo" >
      <ImageBlock v-for="(item, index) in items" v-bind:key="item.url + '-' + index" :item="item" />
    </div>
  </div>
</template>

<script>
  import InputForm from './components/InputForm.vue'
  import ImageBlock from './components/ImageBlock.vue'

  export default {
    name: 'App',
    components: {
      InputForm,
      ImageBlock
    },
    data() {
      return {
        items: []
      }
    },
    methods: {
      load(evt) {
        JSON.parse(evt).galleryImages.forEach(x => this.addImage(x));
      },
      clear() {
        this.items = []
      },
      get(val) {
        const isJson = data => {
          try {
            JSON.parse(data);
          } catch (e) {
            return false;
          }
          return true;
        }

        if(val) {
          const root = this;
          let xhr = new XMLHttpRequest();
          xhr.open('GET', val);
          xhr.send();
          xhr.onload = function() {
            if(isJson(xhr.response)) {
              let jsonParse = JSON.parse(xhr.response);
              if (jsonParse.galleryImages) {
                jsonParse.galleryImages.forEach(x => root.addImage(x));
              }
            } else {
              root.addImage({url: val});
            }
          };
          xhr.error = function() {
            console.log("can't load image");
          }
        }
      },
      addImage(val) {
        this.items.push(val);
      }
    }
  }
</script>
<style lang="scss" src="@/assets/style/main.scss"></style>