<template>
  <div @mouseenter="$emit('mouseenter')" @mouseleave="$emit('mouseleave')">
    <!-- Message -->
    <p v-if="message">{{ message }}</p>

    <!-- Label -->
    <label>
      <p>
        {{ label }} <span style="color: red;" v-if="required == true">*</span>
      </p>
    </label>
    <!-- Box input -->
    <div>
      <div class="vfi-layout">
        <!-- Real input -->
        <slot />
      </div>
    </div>

    <!-- Error -->
    <p v-if="error && showErrors" style="color: red">
      {{ error }}
    </p>
  </div>
</template>

<script>
export default {
  props: {
    label: null,
    message: null,
    id: null,
    error: null,
    showErrors: { default: true },
    required: { default: false },
    height: { default: "8" },
    minHeight: { default: null },
  },
};
</script>

<style>
/* target the input inside to modify the input */
.vfi-layout input {
  border: 1px solid black;
  outline: none;
  padding: 0.5rem;
  font-size: 1rem;
  font-family: inherit;
  background-color: transparent;
  border-radius: 5px;
}
</style>
