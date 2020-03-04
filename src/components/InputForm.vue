<template>
  <div class="form">
    <div class="form__text-area">
      <input type="text" class="form__input" v-model="link" placeholder="Введите ссылку">
    </div>
    <div class="form__buttons">
      <button type="button" @click.prevent="get" class="form__button">Загрузить</button>
      <button type="button" @click.prevent="clear" class="form__button">Очистить</button>
    </div>
    <div class="form__loadfile">
      <input type="file" class="form__file" @change="loadFile">
    </div>
  </div>
</template>

<script>
  export default {
    name: 'InputForm',
    props: {
      msg: String
    },
    data() {
      return {
        link: ""
      }
    },
    methods: {
      get() {
        if (this.link) {
          this.$emit('get', this.link);
          this.link = "";
        }
      },
      clear() {
        this.link = "";
        this.$emit('clear');
      },
      loadFile(evt) {
        const file = evt.target.files[0];
        const reader = new FileReader();

        reader.onload = e => {
          this.$emit("load", e.target.result);
          evt.target.value = '';
        }
        reader.readAsText(file);
      }
    }
  }
</script>