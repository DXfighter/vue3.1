<template>
  <div class="relative my-4">
    <label
      for="name"
      class="
        absolute
        -top-2
        left-2
        inline-block
        bg-white
        px-1
        text-xs
        font-medium
      "
      :class="{
        'text-red-500':
          !isEmailValid && isAttempted && (email.trim() !== '' || isRequired),
        'text-gray-500': isEmailValid || !isAttempted,
      }"
    >
      E-Mail Adresse
    </label>

    <input
      type="text"
      name="name"
      id="name"
      v-model="email"
      @input="validateEmail"
      @blur="attemptValidation"
      :class="[
        'block',
        'w-full',
        'rounded-md',
        'border',
        'py-1.5',
        'text-gray-900',
        'shadow-sm',
        'ring-1',
        'ring-inset',
        'ring-gray-300',
        'placeholder:text-gray-400',
        'focus:ring-2',
        'focus:ring-inset',
        'focus:ring-indigo-600',
        'sm:text-sm',
        'sm:leading-6',
        {
          'border-red-500':
            !isEmailValid && isAttempted && (email.trim() !== '' || isRequired),
          'border-gray-300': isEmailValid || !isAttempted,
        },
      ]"
      placeholder="Email"
    />

    <p
      v-if="
        !isEmailValid &&
        (((email.trim() !== '' || !isRequired) && isAttempted) || email === '')
      "
      class="my-3 text-sm text-red-500"
    >
      {{ email === '' ? '' : 'Please enter a valid email address.' }}
    </p>

    <p
      v-if="isRequired && !isEmailValid && email.trim() === '' && isAttempted"
      class="my-3 text-sm text-red-500"
    >
      {{ 'Email is required.' }}
    </p>
  </div>
</template>

<script lang="ts">
export default {
  name: 'LtEmailInput',
  props: {
    isRequired: {
      type: Boolean,
      default: false,
    },
  },
  data() {
    return {
      email: '',
      isEmailValid: true,
      isAttempted: false,
    };
  },
  methods: {
    validateEmail() {
      const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
      this.isEmailValid = emailRegex.test(this.email);

      if (this.isAttempted && this.isEmailValid) {
        this.isAttempted = false;
      }
    },
    attemptValidation() {
      this.isAttempted = true;
    },
  },
};
</script>
