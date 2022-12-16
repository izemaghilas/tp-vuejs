<template>
  <div>
    <label :for="name">{{ name }}</label>
    <input
      :id="name"
      :name="name"
      :type="type"
      :value="name"
      @input="handleChange"
      @blur="handleBlur"
    />
  </div>
</template>

<script>
import { ref } from "vue";

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
    const values = ref(attrs.values);
    const errors = ref(attrs.errors);
    const touched = ref(attrs.touched);

    function handleChange(event) {
      const { name, value } = event.target;
      values.value[name] = value;
      emit("update:values", values.value);
    }

    function handleBlur(event) {
      const { name } = event.target;
      touched.value[name] = true;
      emit("update:touched", touched.value);
      errors.value[name] = attrs.validate(values.value)[name];
      emit("update:errors", errors.value);
    }

    return {
      values,
      errors,
      touched,
      handleChange,
      handleBlur,
    };
  },
};
</script>
