<template>
  <div
    v-if="showModal"
    class=" obid fixed inset-0 flex items-end justify-center z-50 bg-black bg-opacity-50 transition-all duration-2000 ease-in-out"
  >
    <div
    
      class="bg-white w-full pt-10 px-6 rounded-t-lg shadow-lg h-4/6 relative transition-all duration-2000 ease-in-out"
    >
      <button
        @click="closeModal"
        class="absolute top-0 right-0 m-2 bg-orange-100 text-black px-4 py-1 rounded m-6 hover:text-white hover:bg-orange-400"
      >
        X
      </button>

      <p class="text-xs">Xarid</p>
      <div class="flex justify-between items-center w-full my-2">
        <span class="text-xl">{{ selectedItem.stock.issue_name }}</span>
        <span class="text-red-600">-{{ selectedItem.overall }} UZS</span>
      </div>
      <div class="flex justify-between items-center w-full mb-3">
        <span class="text-gray-500 text-xs">
          <!-- <span v-if="selectedItem.type === 'buy-limit'">Xarid</span> -->
          <!-- <span v-if="selectedItem.type === 'sell-market'">Sotish</span> -->
          {{ formatTimestamp(selectedItem.updated_on) }}
        </span>

        <span>{{ selectedItem.rfb_finished_on }}</span
        ><span class="text-xs">
          <span class="text-red-600" v-if="selectedItem.status === 'canceled'"
            >Bekor qilingan</span
          >
          <span class="text-gray-600" v-if="selectedItem.status === 'error'"
            >Xatolik</span
          >
          <span class="text-green-500" v-if="selectedItem.status === 'approved'"
            >Muvoffaqiyatli</span
          >
          <span
            class="text-orange-500"
            v-if="selectedItem.status === 'processing'"
            >Birjaga joylashtirilgan</span
          >
        </span>
      </div>
      <div
        class="flex justify-between items-center w-full my-2 rounded-2xl border-solid border-2 border-gray-300 py-1 px-4"
      >
        <span class="text-ms text-black font-semibold">Miqdor</span
        ><span class="text-ms">{{ selectedItem.qty }} ta </span>
      </div>
      <div
        class="flex justify-between items-center w-full my-2 rounded-2xl border-solid border-2 border-gray-300 py-1 px-4"
      >
        <span class="text-ms text-black font-semibold">Bitim narxi</span
        ><span class="text-ms text-black font-bold"
          >{{ selectedItem.price }} UZB</span
        >
      </div>
      <div
        class="flex justify-between items-center w-full my-2 rounded-2xl border-solid border-2 border-gray-300 py-1 px-4"
      >
        <span class="text-ms text-black font-semibold">Bitim miqdor</span
        ><span class="text-ms">{{ selectedItem.total }} UZB</span>
      </div>
      <div
        class="flex justify-between items-center w-full my-2 rounded-2xl border-solid border-2 border-gray-300 py-1 px-4"
      >
        <span class="text-ms text-black font-semibold">Kamissiya</span
        ><span class="text-ms">{{ selectedItem.interest }} UZB</span>
      </div>
      <div
        class="flex justify-between items-center w-full my-2 rounded-2xl border-solid border-2 border-gray-300 py-1 px-4"
      >
        <span class="text-ms text-black font-semibold">Jami</span
        ><span class="text-ms">{{ selectedItem.overall }} UZB</span>
      </div>
      <button
        v-if="selectedItem.status === 'error'"
        class="w-full bg-orange-100 p-3 rounded-md my-3"
      >
        Null
      </button>
      <button
        @click="openModalCenter"
        v-if="selectedItem.status === 'canceled'"
        class="w-full bg-green-400 p-3 rounded-md my-3"
      >
        <div>Takrorlash</div>
      </button>
      <ModalCenter
        v-if="showModalCenter"
        @close="closeModalCenter"
        @confirm="handleConfirm"
      />
    </div>
  </div>
</template>

<script>
import moment from "moment";
import ModalCenter from "./ModalCenter.vue";
export default {
  components: {
    ModalCenter,
  },
  data() {
    return {
      showModalCenter: false,
    };
  },
  props: {
    showModal: {
      type: Boolean,
      default: true,
    },
    selectedItem: {
      type: Object,
      default: () => ({}),
    },
  },
  methods: {
    closeModal() {
      this.$emit("close");
    },
    formatTimestamp(time) {
      return moment(time).format("HH:mm DD.MM.YYYY");
    },
    openModalCenter() {
      this.showModalCenter = true;
    },
    closeModalCenter() {
      this.showModalCenter = false;
    },
    handleConfirm() {
      alert("Yaratildi");
    },
  },
};
</script>
<style scoped>
.obid{
  transition: transform 2s ease-in-out;
}
</style>
