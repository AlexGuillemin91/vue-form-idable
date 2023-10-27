<template>
  <input type="text" :value="value" :placeholder="placeholder" :disabled="disabled" />
</template>

<script>
export default {
  props: {
    value: null,
    placeholder: null,
    disabled: false
  }
}
</script>
