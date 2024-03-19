<template>
  <div>
    <div class="modal-container">
      <a class="filter-icon">Filter </a>
    </div>
    <div class="modal" id="modalbox2" data-transition="right">
      <a href="#" data-button="close">X<span>=></span></a>
    </div>
    <h1>Modal Bottom</h1>
  </div>
</template>
<script>
export default {
  data() {
    return {};
  },
};
</script>
<style scoped>
@import url(https://fonts.googleapis.com/css?family=Overlock);

.custom-btn {
  width: 100%;
  height: 40px;
  color: #fff;
  border-radius: 5px;
  padding: 10px 25px;
  font-family: "Lato", sans-serif;
  font-weight: 500;
  background: transparent;
  cursor: pointer;
  transition: all 0.3s ease;
  position: relative;
  display: inline-block;
  box-shadow: inset 2px 2px 2px 0px rgba(255, 255, 255, 0.5),
    7px 7px 20px 0px rgba(0, 0, 0, 0.1), 4px 4px 5px 0px rgba(0, 0, 0, 0.1);
  outline: none;
}

.modal {
  z-index: 9999;
  position: fixed;
  padding: 50px;
  display: block;
  width: 100%;
  height: 100vh;
  border-radius: 10px;
  overflow: auto;
  background: #fff;
  color: #000;
  transition: all 0.7s;
}
.filter-icon {
  text-decoration: none;
  margin-right: 5px;
  padding: 5px 10px;
  background-color: #0fb668;
  color: white;
  border-radius: 5px;
}

:target {
  left: 0 !important;
  top: 0 !important;
  visibility: visible !important;
  width: 100% !important;
  height: 100% !important;
  opacity: 1 !important;
}

[data-transition="right"] {
  left: 100%;
  top: 0;
}

.modal [data-button="close"] {
  top: 5px;
  right: 5px;
  position: absolute;
  padding: 5px 12px;
  border-radius: 5px;
  -moz-box-shadow: 1px 1px 3px #000;
  -webkit-box-shadow: 1px 1px 3px #000;
  box-shadow: 1px 1px 3px #000;
  color: #fff;
  background: #15a782;
  font-weight: bold;
  font-size: 15px;
  text-decoration: none;
  text-align: center;
}

.modal [data-button="close"]:hover {
  background: #0fb668;
  color: #000066;
}
</style>
