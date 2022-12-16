<template>
  <div>
    <label :for="name">{{ name }}</label>
    <input
      :id="name"
      :name="name"
      :type="type"
      :value="value"
      @input="handleChange"
      @blur="handleBlur"
    />
  </div>
</template>

<script>
import { ref, inject } from "vue";

export default {
  props: {
    name: {
      type: String,
      required: true,
    },
    type: {
      type: String,
      required: true,
    },
  },
  setup(props, { emit, attrs }) {
    const initialValues = inject('inital:values')
    const values = ref(attrs.values);
    const errors = ref(attrs.errors);
    const value = initialValues[props.name]

    function handleChange(event) {
      const { name, value } = event.target;
      values.value[name] = value;
      emit("update:values", values.value);
    }

    function handleBlur(event) {
      const { name } = event.target;
      errors.value[name] = attrs.validate(values.value)[name];
      emit("update:errors", errors.value);
    }

    return {
      values,
      errors,
      handleChange,
      handleBlur,
      value,
    };
  },
};
</script>
