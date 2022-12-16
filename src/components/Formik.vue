<template>
  <form @submit.prevent="handleSubmit">
    <slot :values="values" :errors="errors" :isSubmitting="isSubmitting" :handleSubmit="handleSubmit" />
  </form>
</template>

<script>
import { ref, provide } from "vue";

export default {
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
    let isSubmitting = false;
    provide('inital:values', props.initialValues)


    function handleSubmit(event) {
      isSubmitting = true;
      event.preventDefault();
      props.onSubmit(values.value);
      isSubmitting = false;
    }

    return {
      values,
      errors,
      handleSubmit,
      isSubmitting,
    };
  },
};
</script>
