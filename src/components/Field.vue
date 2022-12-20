<template>
  <component :is="as" v-model="value" :name="name" :error="error" />
</template>

<script>
export default {
  name: "field",
  props: {
    name: {
      type: String,
      required: true,
    },
    as: {
      type: String,
      required: true,
    },
  },
  inject: ["formik"],
  computed: {
    value: {
      get() {
        return this.formik.values[this.name];
      },
      set(value) {
        this.formik.values = { ...this.formik.values, [this.name]: value };
      },
    },
    error() {
      return this.formik.errors[this.name];
    },
  },
};
</script>
