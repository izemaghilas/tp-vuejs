<template>
  <form @submit.prevent="handleSubmit">
    <button type="submit">Submit</button>
  </form>
</template>

<script>
import { ref } from "vue";

export default {
  name: "Formik",
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
  setup(props) {
    const values = ref(props.initialValues);
    const errors = ref({});
    const touched = ref({});

    function handleChange(event) {
      const { name, value } = event.target;
      values.value[name] = value;
    }

    function handleBlur(event) {
      const { name } = event.target;
      touched.value[name] = true;
      errors.value[name] = props.validate(values.value)[name];
    }

    function handleSubmit(event) {
      event.preventDefault();
      props.onSubmit(values.value);
    }

    return {
      values,
      errors,
      touched,
      handleChange,
      handleBlur,
      handleSubmit,
    };
  },
};
</script>
