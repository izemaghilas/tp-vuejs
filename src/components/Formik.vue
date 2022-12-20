<template>
  <form @submit.prevent="handleSubmit">
    <slot />
  </form>
</template>

<script>
export default {
  name: "formik",
  props: {
    initialValues: {
      type: Object,
      required: true,
    },
    validate: {
      type: Function,
      required: true,
    },
    onSubmit: {
      type: Function,
      required: true,
    },
  },
  data() {
    return {
      values: {},
      errors: {},
      isSubmitting: false,
    };
  },
  created() {
    this.values = this.initialValues;
    this.errors = this.validate(this.values);
  },
  methods: {
    handleSubmit() {
      this.isSubmitting = true;
      this.errors = this.validate(this.values);
      if (Object.keys(this.errors).length === 0) {
        this.onSubmit(this.values);
      } else {
        this.isSubmitting = false;
      }
    },
  },
  provide() {
    return {
      formik: {
        values: this.values,
        errors: this.errors,
        isSubmitting: this.isSubmitting,
      },
    };
  },
};
</script>
