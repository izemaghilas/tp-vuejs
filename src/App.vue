<template>
  <Formik
    :initialValues="{ name: '', email: '', password: '' }"
    :validate="validate"
    :onSubmit="handleSubmit"
  >
    <Field name="name" type="text" />
    <br />
    <Field name="name" type="text" />
    <br />
    <button type="submit">Submit</button>
  </Formik>
</template>

<script>
import Formik from "./components/Formik.vue";
import Field from "./components/Field.vue";

export default {
  name: "App",
  components: {
    Formik,
    Field,
  },
  methods: {
    validate(values) {
      const errors = {};
      if (!values.name) {
        errors.name = "Required";
      }
      if (!values.email) {
        errors.email = "Required";
      } else if (
        !/^[A-Z0-9._%+-]+@[A-Z0-9.-]+\.[A-Z]{2,}$/i.test(values.email)
      ) {
        errors.email = "Invalid email address";
      }
      if (!values.password) {
        errors.password = "Required";
      }
      return errors;
    },
    handleSubmit(values) {
      console.log("clicked submit", values);
    },
  },
};
</script>
