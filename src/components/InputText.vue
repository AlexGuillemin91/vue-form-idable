<template>
  <InputLayout :label="label" :message="message">
      <input ref="input" type="text" :value="value" :placeholder="placeholder" :disabled="disabled" />
  </InputLayout>
</template>

<script>
import InputLayout from './InputLayout.vue';
export default {
  props: {
    label: null,
    message: null,
    value: null,
    placeholder: null,
    disabled: false
  },
  components: {
    InputLayout
  },
}
</script>
