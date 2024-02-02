<script setup>
import InputText from "./components/InputText.vue";
import InputEmail from "./components/InputEmail.vue";
import InputPassword from "./components/InputPassword.vue";
import Form from "./components/Form.vue";
import InputTextArea from "./components/InputTextArea.vue";
</script>

<template>
  <Form @validated="login" :refs="refs" :formError="formError">
    <InputText ref="1" v-model="form.nom" label="Nom" placeholder="test" :required="true"/>
    <InputEmail ref="2" v-model="form.email" label="Email" placeholder="email@email.fr" />
    <InputPassword ref="3" v-model="form.password" label="Mot de passe" />
    <InputTextArea ref="4" v-model="form.message" label="Message" :required="true"/>  
    <button type="submit">Envoyer</button>
  </Form>
</template>

<script>
  export default {
  data() {
    return {
      form: {
        nom: '',
        email: '',
        password: '',
        message: '',
      },
      refs: null,
      formError: null
    };
  },
  mounted() {
    this.refs = this.$refs;
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
