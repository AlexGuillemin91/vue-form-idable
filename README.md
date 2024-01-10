# [Vue 3 FormIdable](https://www.npmjs.com/package/vue3-form-idable)

Vue 3 FormIdable is a Vue 3 component library for creating forms with ease.
Our goal is to make it as easy as possible to create forms with validation and components that can be easily customized.

## Installation

- Clone the repo on your local machine using `git clone`
- Run `npm install` to install all dependencies
- Run `npm run dev` to start the development server or `npm run build` to build the library

## Example

Here is a simple example of how to use the form component with only en email and password field.

```vue

<template>
  <Form @validated="register" :formError ="formError">
    <InputEmail v-model="form.email" label="Email" placeholder="email@email.fr" :required="true"/>
    <InputPassword v-model="form.password" label="Mot de passe" />
    <button type="submit">Envoyer</button>
  </Form>
</template>

<script>
  export default {
  data() {
    return {
      form: {
        email: '',
        password: '',
      },
      formError: null
    };
  },
    methods: {
    async register() {
      // Your form submission logic goes here
    }
    }
  }
</script>
    
```

We are providing a list of different components that you can discover just below.

## Components

```vue
<InputText />       // Default input
<InputEmail />      // Input with email validation
<InputPassword />   // Input with password validation (used for register form)
<InputSecret />     // Input used when you want to hide the value (login, password confirmation...)
```

Each component goes with a lot of props : 

```vue
label: { type: String, default: "" },
modelValue: { default: "" },
min: { type: Number, default: null },
max: { type: Number, default: 256 },
required: { type: Boolean, default: false },
placeholder: { type: String, default: "" },
disabled: { type: Boolean, default: false },
message: { type: String, default: "" },
showErrors: { type: Boolean, default: true },
```

It is easier to taget a specific error with the props you want to check.
