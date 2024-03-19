<template>
  <div
    v-if="filterModal"
    class="fixed inset-0 flex items-end justify-center z-20 bg-black bg-opacity-50 transition-all duration-2000 ease-in-out"
  >
    <div
      class="bg-white w-full py-3 px-4 rounded-t-lg shadow-lg h-full relative"
    >
      <div class="flex items-center justify-between">
        <img
          @click="closeFilter"
          src="./images/back-arrow.png"
          width="25"
          class="cursor-pointer"
        />
        <h1 class="text-sl">Filter</h1>
        <button
          @click="closeFilter"
          class="text-green-500 px-4 py-1 rounded mt-3 hover:bg-green-200 hover:text-black"
        >
          Tozalash
        </button>
      </div>
      <div class="filter-box">
        <div class="my-5">
          <h1 class="header-text">Qimmatli qog'ozlar</h1>
          <div class="flex flex-wrap items-center">
            <div>
              <input
                type="checkbox"
                id="metal"
                class="hidden-checkbox"
                v-model="checkedNames"
                name="preferred"
                value="0"
                @change="onChangeHandler"
              />
              <label for="metal" class="checkbox-button text-gray-400">
                Oddiy aktsiyalar
              </label>
            </div>
            <div>
              <input
                type="checkbox"
                id="preferred"
                class="hidden-checkbox"
                v-model="checkedNames"
                name="preferred"
                value="1"
                @change="onChangeHandler"
              />
              <label for="preferred" class="checkbox-button text-gray-400">
                Afzallikli aktsiyalar
              </label>
            </div>
            <div>
              <input
                type="checkbox"
                id="checkbox3"
                class="hidden-checkbox"
                v-model="checkedNames"
                name="market_code"
                value="BND"
                @change="onChangeHandler"
              />
              <label for="checkbox3" class="checkbox-button text-gray-400"
                >Obligatsiyala</label
              >
            </div>
          </div>
        </div>
        <hr />
        <div class="mb-4">
          <h1 class="header-text">Bozor</h1>
          <div class="flex flex-wrap">
            <div>
              <input
                type="checkbox"
                id="checkbox1"
                class="hidden-checkbox"
                v-model="checkedNames"
                name="market_code"
                value="STK"
                @change="onChangeHandler"
              />
              <label for="checkbox1" class="checkbox-button text-gray-400"
                >STK</label
              >
            </div>
            <div>
              <input
                type="checkbox"
                id="checkbox2"
                class="hidden-checkbox"
                v-model="checkedNames"
                name="market_code"
                value="SMS"
                @change="onChangeHandler"
              />
              <label for="checkbox2" class="checkbox-button text-gray-400"
                >SMS</label
              >
            </div>
            <div>
              <input
                type="checkbox"
                id="BND"
                class="hidden-checkbox"
                v-model="checkedNames"
                name="market_code"
                value="BND"
                @change="onChangeHandler"
              />
              <label for="BND" class="checkbox-button text-gray-400">BND</label>
            </div>
            <div>
              <input
                type="checkbox"
                id="checkbox4"
                class="hidden-checkbox"
                v-model="checkedNames"
                name="market_code"
                value="SMB"
                @change="onChangeHandler"
              />
              <label for="checkbox4" class="checkbox-button text-gray-400"
                >SMB</label
              >
            </div>
          </div>
        </div>
        <hr />
        <div class="my-4">
          <h1 class="header-text">Tranzaksiya turi</h1>
          <div class="flex flex-wrap items-center">
            <div>
              <input
                type="checkbox"
                id="buy"
                class="hidden-checkbox"
                v-model="checkedNames"
                name="deal_type"
                value="buy"
                @change="onChangeHandler"
              />
              <label for="buy" class="checkbox-button text-gray-400"
                >Xarid
              </label>
            </div>
            <div>
              <input
                type="checkbox"
                id="sell"
                class="hidden-checkbox"
                v-model="checkedNames"
                name="deal_type"
                value="sell"
                @change="onChangeHandler"
              />
              <label for="sell" class="checkbox-button text-gray-400">
                Sotish
              </label>
            </div>
          </div>
        </div>
        <hr />
        <div class="my-4">
          <h1 class="header-text">Buyurtma turi</h1>
          <div class="flex flex-wrap items-center">
            <div>
              <input
                type="checkbox"
                id="market"
                class="hidden-checkbox"
                v-model="checkedNames"
                name="order_type"
                value="market"
                @change="onChangeHandler"
              />
              <label for="market" class="checkbox-button text-gray-400">
                Bozor turi
              </label>
            </div>
            <div>
              <input
                type="checkbox"
                id="limit"
                class="hidden-checkbox"
                v-model="checkedNames"
                name="order_type"
                value="limit"
                @change="onChangeHandler"
              />
              <label for="limit" class="checkbox-button text-gray-400">
                Cheksiz
              </label>
            </div>
          </div>
        </div>
        <hr />
        <div class="my-4">
          <h1 class="header-text">Holat</h1>
          <div class="flex flex-wrap items-center">
            <div>
              <input
                type="checkbox"
                id="approved"
                class="hidden-checkbox"
                v-model="checkedNames"
                name="status"
                value="approved"
                @change="onChangeHandler"
              />
              <label for="approved" class="checkbox-button text-gray-400"
                >Muvaffaqiyatli
              </label>
            </div>
            <div>
              <input
                type="checkbox"
                id="canceled"
                class="hidden-checkbox"
                v-model="checkedNames"
                name="status"
                value="canceled"
                @change="onChangeHandler"
              />
              <label for="canceled" class="checkbox-button text-gray-400">
                Bekor qilinga
              </label>
            </div>
            <div>
              <input
                type="checkbox"
                id="error"
                class="hidden-checkbox"
                v-model="checkedNames"
                name="status"
                value="error"
                @change="onChangeHandler"
              />
              <label for="error" class="checkbox-button text-gray-400">
                Xatolik</label
              >
            </div>
          </div>
        </div>
        <hr />
      </div>
      <button
        @click="closeFilter"
        type="button"
        class="focus:outline-none w-full text-white bg-green-500 hover:bg-green-600 focus:ring-4 focus:ring-green-300 font-medium rounded-lg text-sm px-5 py-3 my-4 dark:bg-green-500 dark:hover:bg-green-600 dark:focus:ring-green-800"
      >
        Qo'llash
      </button>
    </div>
  </div>
</template>
<script>
export default {
  props: {
    myFunction: {
      type: Function,
      required: true,
    },
    filterModal: {
      type: Boolean,
      default: true,
    },
  },

  data() {
    return {
      checkedNames: [],
      isChecked: true,
      formData: {},
    };
  },

  methods: {
    closeFilter() {
      this.$emit("close");
      this.myFunction(this.formData);
    },

    onChangeHandler(event) {
      this.formData[event.target.name] = event.target.value;
    },
  },
};
</script>
<style scoped>
.checkbox-button {
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 5px 20px;
  border: none;
  outline: none;
  border-radius: 15px;
  margin-right: 20px;
  cursor: pointer;
  background-color: #f5f5f5;
  transition: all 0.2s ease-in-out;
}
.hidden-checkbox {
  display: block;
  opacity: 0;
}
.hidden-checkbox:checked + .checkbox-button {
  background-color: #8f98a5;
  color: #ffffff; /* Blue for checked state */
}
.header-text {
  font-size: 19px;
  font-weight: 600;
  color: #8f98a5;
}

.filter-box {
  height: calc(100vh - 160px);
  overflow: auto;
  padding-bottom: 60px;
}
.filter-item {
  display: flex;
  flex-wrap: wrap;
}

.modal {
  z-index: 9999;
  position: fixed;
  padding: 10px;
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
.close-box {
  display: flex;
  justify-content: space-between;
  width: 100%;
  height: 30px;
  align-items: center;
  margin-bottom: 20px;
}

.modal [data-button="close"]:hover {
  background: #0fb668;
  color: #000066;
}

/* checkbox */
/* Hide the original checkbox */
.button-checkbox input[type="checkbox"] {
  opacity: 0; /* Completely transparent */
  position: absolute; /* Allow positioning over it */
}

/* Style the checkbox container as a button */
.data {
  width: 100%;
}
.button-checkbox {
  border-radius: 15px;
  font-size: 16px;
  line-height: 110%;
  padding: 8px 15px;
  margin-right: 15px;
  margin-bottom: 15px;
  cursor: pointer;
  background: #dfe2e6;
  color: #ffffff;
}
.true {
  background-color: #bfc4c1;
}
.false {
  background-color: #4c5152;
}

/* checkbox */
</style>
