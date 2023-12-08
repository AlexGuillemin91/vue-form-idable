<template>
  <form @submit.prevent="onSubmit">
    <slot />
  </form>
</template>

<script setup>
import { ref } from 'vue';

const formRefs = ref([]);

const addRef = (refInstance) => {
  formRefs.value.push(refInstance);
};

const validateForm = () => {
  const checks = [];
  formRefs.value.forEach((input) => {
    checks.push(input.validate());

    input.$children.forEach((inp) => {
      checks.push(inp.validate());
    });
  });
  return !checks.includes(false);
};

const onSubmit = () => {
  if (validateForm()) {
    console.log('Formulaire soumis avec succès.');
  } else {
    console.log('Le formulaire contient des erreurs.');
  }
};
</script>
