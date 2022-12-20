<template>
  <div>
    <img
      src="https://images.pexels.com/photos/3225517/pexels-photo-3225517.jpeg?auto=compress&cs=tinysrgb&w=1260&h=750&dpr=1"
    />
    <input type="text" v-model="captchaValue" />
  </div>
</template>

<script>
export default {
  name: "Captcha",
  data() {
    return {
      captchaValue: "",
    };
  },
  methods: {
    refreshCaptcha() {},
  },
};
</script>
