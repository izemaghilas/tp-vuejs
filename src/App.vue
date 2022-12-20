<template>
  <Formik
    :initialValues="{ email: '', password: '' }"
    :validate="validate"
    :onSubmit="submitForm"
  >
    <h1>Values</h1>
    {{ JSON.stringify(values) }}
    <h1>Errors</h1>
    {{ JSON.stringify(errors) }}
    <Field type="email" name="email" as="input" />
    <Field type="password" name="password" as="input" />
    <Field type="password" name="password" as="Captcha" />
    <button type="submit" :disabled="isSubmitting">Submit</button>
  </Formik>
</template>

<script>
import Formik from "./components/Formik.vue";
import Field from "./components/Field.vue";
import Captcha from "./components/Captcha.vue";

export default {
  name: "app",
  components: {
    Formik,
    Field,
    Captcha,
  },
  data() {
    return {
      values: {
        email: "",
        password: "",
      },
      errors: {},
      isSubmitting: false,
    };
  },
  methods: {
    validate(values) {
      const errors = {};
      if (!values.email) {
        errors.email = "Required";
      } else if (
        !/^[A-Z0-9._%+-]+@[A-Z0-9.-]+\.[A-Z]{2,}$/i.test(values.email)
      ) {
        errors.email = "Invalid email address";
      }
      return errors;
    },
    submitForm(values) {
      console.log("submitting");
      this.isSubmitting = true;
      setTimeout(() => {
        alert(JSON.stringify(values, null, 2));
      }, 5000);
      this.isSubmitting = false;
    },
  },
};
</script>
