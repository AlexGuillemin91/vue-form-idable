<template>
  <div @mouseenter="$emit('mouseenter')" @mouseleave="$emit('mouseleave')" @click="$emit('click')">
    <!-- Message -->
    <p v-if="message">{{ message }}</p>

    <!-- Label -->
    <label>
      <p>
        {{ label }}
      </p>
    </label>
    <!-- Box input -->
    <div>
      <div>
        <!-- Real input -->
        <slot />
      </div>
    </div>

    <!-- Error -->
    <p v-if="error && showErrors">
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
