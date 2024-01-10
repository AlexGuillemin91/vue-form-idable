<template>
  <form ref="form" @submit.prevent="onSubmit">
    <slot></slot>
  </form>
</template>

<script>
export default {
  props: {
    refs: { type: Object, default: {} },
  },
  methods: {
    validateForm() {
      const checks = [];
      for (const r in this.refs) {
        console.log('r', r);
        try {
          checks.push(this.refs[r].isValidated());
        } catch { }
      }
      return !checks.includes(false);
    },
    onSubmit(event) {
      event.preventDefault();
      console.log('coucou');
      this.validateForm() ? this.$emit("validated") : null;
    },
  }
};
</script>

