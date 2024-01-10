<template>
  <InputLayout :label="label" :message="message" :error="error" :showErrors="showErrors" :required="required"
    @mouseenter="$emit('mouseenter')" @mouseleave="$emit('mouseleave')" @click="$emit('click')">
    <input ref="inputForm" type="email" :value="modelValue" :placeholder="placeholder" :disabled="disabled" :required="required"
      @input="$emit('update:model-value', $event.target.value)" @blur="validate()" />
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
      return REGEX_EMPTY.test(this.modelValue);
    },
    isValidated() {
      return this.validate()
    }
  },
  methods: {
    validate() {
      this.error = null;
      console.log('validate', this.modelValue);
      console.log('label', this.label);

      // Règle requise
      if (this.required && this.isEmpty) {
        this.error = 'Ce champ est requis';
        return false;
      }

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
    }
  },
};
</script>
