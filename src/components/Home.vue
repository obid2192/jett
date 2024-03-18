<template>
  <div>
    <div class="w-full flex justify-center items-center p-5">
      <img :src="img" alt="logo" width="100%" />
    </div>
    <div>
      <OhVueIcon icon="io-home" />
    </div>
  </div>
</template>
<script>
export default {
  data() {
    return {
      img: "https://dev-front.jett.uz/img/social_uz.75b5c3b9.svg",
    };
  },
};
</script>
<style scoped></style>
