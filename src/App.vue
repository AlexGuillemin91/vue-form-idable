<script setup>
import InputText from "./components/InputText.vue";
import Form from "./components/Form.vue";
</script>

<template>
  <Form @validated="login" :formError ="formError">
    <InputText v-model="form.nom" label="Nom" placeholder="test" :required="true"/>
    <InputText v-model="form.prenom" label="Prénom" placeholder="test" />
    <button type="submit">Envoyer</button>
  </Form>
</template>

<script>
  export default {
  data() {
    return {
      form: {
        nom: '',
        prenom: '',
      },
      formError: null
    };
  },
    methods: {
    async login() {
      // Your form submission logic goes here
      try {
        // Example: Simulate an async API call
        await new Promise((resolve) => setTimeout(resolve, 1000));
        console.log('Form submitted:', this.form);
        this.formError = null; // Clear any previous form errors
      } catch (error) {
        this.formError = 'Une erreur s\'est produite lors de la soumission du formulaire.';
        console.error(error);
      }
    }
    }
  }
</script>

<style scoped></style>
