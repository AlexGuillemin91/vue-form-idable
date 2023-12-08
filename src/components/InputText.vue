<template>
  <InputLayout :label="label" :message="message" :error="error" :showErrors="showErrors" :required="required"
          @mouseenter="$emit('mouseenter')" @mouseleave="$emit('mouseleave')" @click="$emit('click')">
      <input ref="input" type="text" :value="modelValue" :placeholder="placeholder" :disabled="disabled" @input="$emit('update:model-value', $event.target.value)"
              @change="handleChange" @blur="handleBlur"/>
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
    handleChange(event) {
      this.$emit('update:model-value', event.target.value);
      this.checkIsValidated();
    },
    handleBlur(event) {
      this.$emit('blur', event.target.value);
    },
    checkIsValidated() {
      this.error = null;
      console.log('check for errors');
      // Required rule
      if (this.required && this.isEmpty) {
        console.log(this.isEmpty);
        console.log("mais frerot stp");
        this.error = "Ce champ est requis"
        return false;
      }
      // Min rule
      if (this.min && this.modelValue.length < this.min) {
        this.error = "Ce champ doit contenir au moins " + this.min + " caractères"
        return false
      }
      // Max rule
      if (this.max && this.modelValue.length > this.max) {
        this.error = "Ce champ doit contenir au maximum " + this.max + " caractères"
        return false
      }

      return true;
    },
  },
}
</script>
