<template>
  <form @submit.prevent="onSubmit">
    <slot />
  </form>
</template>

<script>
export default{
  props: {
    refs: { type: Object, default: {} },
  },
  methods: {
    validate() {
      const checks = [];
      for (const r in this.refs) {
        try {
          checks.push(this.refs[r].validate());
        } catch { }
      }
      return !checks.includes(false);
    },
    onSubmit(event) {
      event.preventDefault();
      this.validate() ? this.$emit("validated") : null;
    },
  },
};
</script>

