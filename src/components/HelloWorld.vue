<template>
  <div id="app">
    <h4>option: numeric and max:length</h4>
    <p>
      <input v-validate="'numeric|max:10'" type="text" name="num1">
      <br>
      <span v-if="errors.has('num1')">{{ errors.first('num1') }}</span>
    </p>

    <h4>option: numeric and max_value:value</h4>
    <p>
      <input v-validate="'max_value:10'" type="text" name="num2">
      <br>
      <span v-if="errors.has('num2')">{{ errors.first('num2') }}</span>
    </p>

    <h4>option: Regex: ^([0-9]+)$</h4>
    <p>
      <input v-validate="{ required: true, regex: /^([0-9]+)$/ }" name="regex">
      <br>
      <span v-if="errors.has('regex')">{{ errors.first('regex') }}</span>
    </p>

    <button @click="register">Register</button>
  </div>

</template>

<script>
  import Vue from 'vue'
  import VeeValidate from 'vee-validate'

  Vue.use(VeeValidate)

  export default {
    data() {
      return {
        email: ''
      }
    },
    methods: {
      register() {
        this.$validator.validateAll().then(() => {
          alert('Hello, ' + this.email)
        }).catch(() => {
          alert(this.errors.all())
        })
      }
    }
  }
</script>

<style>
  .alert-danger {
    color: red;
  }

  .has-error {
    border-color: red;
  }
</style>
