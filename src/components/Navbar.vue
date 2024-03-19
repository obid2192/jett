<template>
  <div class="container">
    <div class="flex justify-around items-center">
      <div>
        <span>
          <router-link class="flex justify-center items-center flex-col" to="/"
            ><img
              @click="closeFilter"
              src="./images/home.png"
              width="25"
            />
            <div>Asosiy</div></router-link
          ></span
        >
      </div>
      <div>
        <span>
          <router-link class="flex justify-center items-center flex-col" to="/order"
            ><img
              @click="closeFilter"
              src="./images/list.png"
              width="25"
            />
            <div>Bitimlar</div></router-link
          ></span
        >
      </div>
      <div>
        <span
          ><router-link class="flex justify-center items-center flex-col" to="/yana"
            ><img
              @click="closeFilter"
              src="./images/menu.png"
              width="25"
            />
            <div>Yana</div></router-link
          ></span
        >
      </div>
    </div>
  </div>
</template>
<script>
export default {};
</script>
<style scoped>
.container {
  position: absolute;
  left: 0;
  bottom: 0;
  right: 0;
  height: 70px;
  width: 100%;
  position: fixed;
  border-top: 1px solid rgb(209, 206, 206);
  /* box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2), 0 6px 20px 0 rgba(0, 0, 0, 0.19); */
}

</style>
