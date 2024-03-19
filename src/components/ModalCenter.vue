<template>
  <div
    v-if="showModalCenter"
    class="fixed inset-0 flex items-center justify-center z-50 bg-black bg-opacity-50"
  >
    <div class="bg-white shadow-lg max-w-sm grid content-between rounded-md">
      <h1 class="text-xl font-bold text-gray-400 m-4 text-center">
        Xuddi shu shartlar bilan birjada yangi bitim yaratiladi
      </h1>
      <div class="flex justify-around mt-4 bg-orange-100 p-2">
        <button
          @click="closeModalCenter"
          class="px-4 py-2 ml-2 text-red-500 rounded-md"
        >
          Bekor qilish
        </button>
        <button
          @click="$emit('confirm')"
          class="px-4 py-2 text-green-500 rounded-md"
        >
          Yaratish
        </button>
      </div>
    </div>
    
  </div>
</template>

<script>
export default {
  props: {
    showModalCenter: {
      type: Boolean,
      default: true,
    },
  },
  methods: {
    closeModalCenter() {
      this.$emit("close");
    },
  },
};
</script>
