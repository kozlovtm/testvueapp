<template>
  <div class="form">
    <div class="form__text-area">
      <input type="text" class="form__input" v-model="link" placeholder="Введите ссылку">
    </div>
    <div class="form__buttons">
      <button type="button" @click.prevent="get" class="form__button">Загрузить</button>
      <button type="button" @click.prevent="clear" class="form__button">Очистить</button>
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
      }
    }
  }
</script>