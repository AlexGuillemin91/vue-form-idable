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
        try {
          checks.push(this.refs[r].validate());
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

<!-- <script>
import { ref } from 'vue';

const inputForm = ref([]);

const addRef = (refInstance) => {
  inputForm.value.push(refInstance);
};

const validateForm = () => {
  const checks = [];
  console.log(input.value);
  inputForm.value.forEach((input) => {
    checks.push(input.validate());

    input.$children.forEach((inp) => {
      checks.push(inp.validate());
    });
  });
  return !checks.includes(false);
};

const onSubmit = (event) => {
  event.preventDefault();
  console.log('coucou');
  if (validateForm()) {
    console.log('Formulaire soumis avec succès.');
    this.$emit('submit');
  } else {
    console.log('Le formulaire contient des erreurs. Annulation de la soumission du formulaire.');
  }
};

export { addRef, onSubmit };
</script> -->
