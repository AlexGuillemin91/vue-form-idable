<template>
  <InputLayout :label="label" :message="message" :error="error" :showErrors="showErrors" :required="required"
    @mouseenter="$emit('mouseenter')" @mouseleave="$emit('mouseleave')" @click="$emit('click')">
    <input ref="input" type="text" :value="modelValue" :placeholder="placeholder" :disabled="disabled"
        @input="handleInput"
        @blur="validate()"/>
  </InputLayout>
</template>

<script>
import InputLayout from './InputLayout.vue';
import { REGEX_EMPTY } from '../constants/regex';

export default {
  props: {
    label: { type: String, default: "" },
    modelValue: { default: "" },
    min: { type: Number, default: null },
    max: { type: Number, default: 256 },
    required: { type: Boolean, default: false },
    placeholder: { type: String, default: "" },
    disabled: { type: Boolean, default: false },
    message: { type: String, default: "" },
    showErrors: { type: Boolean, default: true },
  },
  data() {
    return {
      error: null,
    };
  },
  components: {
    InputLayout
  },
  computed: {
    isEmpty() {
      console.log(this.modelValue);
      console.log(REGEX_EMPTY.test(this.modelValue));
      return REGEX_EMPTY.test(this.modelValue);
    },
  },
  methods: {
    handleInput(event) {
      this.$emit('update:modelValue', event.target.value);
    },
    validate() {
      console.log('Vérification des erreurs');
      this.error = null;
      console.log('label : ',this.label);
      console.log('requis : ',this.required);
      console.log('vide : ', this.isEmpty);

      // Règle requise
      if (this.required && this.isEmpty) {
        this.error = 'Ce champ est requis';
        return false;
      }
      console.log('erreur : ', this.error);
      // Règle de min
      if (this.min && this.modelValue.length < this.min) {
        this.error = `Ce champ doit contenir au moins ${this.min} caractères`;
        return false;
      }
      // Règle de max
      if (this.max && this.modelValue.length > this.max) {
        this.error = `Ce champ doit contenir au maximum ${this.max} caractères`;
        return false;
      }

      return true;
    },
  },
  };
</script>

