<template>
  <div>
    <div class="search-box">
      <!-- search -->
      <input
        class="search-input"
        type="text"
        v-model="filterText"
        placeholder="Search..."
      />
      <!-- search -->
      <!-- filter -->
      <img @click="openfilter" src="./images/filter.png" width="35" class="cursor-pointer ml-2"/>
      <!-- filter -->
    </div>
    <div>
      <!-- items -->
      <div>
      
      </div>
      <div
        v-for="item in filteredItems"
        :key="item.order_id"
        @click="openModal(item)"
        class="box"
      >
        <div class="logo">
          <img :src="item.stock.logo" alt="logo" height="40" width="40" />
        </div>
        <div class="text-container">
          <div class="text-box">
            <span class="buy">
              <span v-if="item.type === 'buy-limit'">Xarid</span>
              <span v-if="item.type === 'sell-market'">Sotish</span>
              {{ formatTimestamp(item.updated_on) }}
            </span>

            <span>{{ item.rfb_finished_on }}</span
            ><span class="status">
              <span class="canceled" v-if="item.status === 'canceled'"
                >Bekor qilingan</span
              >
              <span class="error" v-if="item.status === 'error'">Xatolik</span>
              <span class="approved" v-if="item.status === 'approved'"
                >Muvoffaqiyatli</span
              >
              <span class="processing" v-if="item.status === 'processing'"
                >Birjaga joylashtirilgan</span
              >
            </span>
          </div>
          <div class="text-box">
            <span class="bank-name">{{ item.stock.issue_name }}</span
            ><span class="total">-{{ item.overall }} UZS</span>
          </div>
          <div class="text-box">
            <span class="aksiya">Aksiyalar: +{{ item.qty }}</span
            ><span class="aksiya-price">{{ item.price }} UZS</span>
          </div>
        </div>
      </div>
      <!-- items -->
      <Modal
        v-if="showModal"
        @close="closeModal"
        :selectedItem="selectedItem"
      />
      <Filter
          v-if="filterModal"
          :myFunction="handleData"
          @close="closeFilter"
        />
    </div>
 
  </div>
</template>
<script>
import { ref } from "vue";
import moment from "moment";
import Filter from "./Filter.vue";
import Modal from "./BottomModal.vue";
import { useRouter } from "vue-router";

const users = ref([
  {
    order_id: 157503,
    preferred: 0,
    stock: {
      id: 5,
      ticker: "UZMK",
      issue_code: "UZ7021720006",
      issue_name: "O'zmetkombinat",
      currency: "uzs",
      logo: "https://jett.uz/upload/logos/UZMK.png",
    },
    repeatable: 0,
    type: "buy-limit",
    market_code: "STK",
    qty: 25,
    price: 6140,
    interest: 1826.65,
    total: 153500,
    overall: 155326.65,
    rfb_created_on: null,
    rfb_finished_on: null,
    rfb_error_reason: null,
    status: "canceled",
    added_on: "2024-03-04T10:30:36.000Z",
    updated_on: "2024-03-04T10:31:40.000Z",
  },
  {
    order_id: 157502,
    preferred: 0,
    stock: {
      id: 3,
      ticker: "URTS",
      issue_code: "UZ7043200003",
      issue_name: "O'zRTXB",
      currency: "uzs",
      logo: "https://jett.uz/upload/logos/URTS.png",
    },
    repeatable: 0,
    type: "buy-limit",
    market_code: "STK",
    qty: 36,
    price: 19700,
    interest: 8439.48,
    total: 709200,
    overall: 717639.48,
    rfb_created_on: null,
    rfb_finished_on: null,
    rfb_error_reason: null,
    status: "processing",
    added_on: "2024-03-04T10:29:24.000Z",
    updated_on: "2024-03-04T10:31:40.000Z",
  },
  {
    order_id: 157501,
    preferred: 0,
    stock: {
      id: 642,
      ticker: "UZTL",
      issue_code: "UZ7047110000",
      issue_name: "O'zbektelekom",
      currency: "uzs",
      logo: "https://jett.uz/upload/logos/UZTL.png",
    },
    repeatable: 0,
    type: "buy-limit",
    market_code: "STK",
    qty: 50,
    price: 5120,
    interest: 3046.4,
    total: 256000,
    overall: 259046.4,
    rfb_created_on: null,
    rfb_finished_on: null,
    rfb_error_reason: null,
    status: "processing",
    added_on: "2024-03-04T10:28:51.000Z",
    updated_on: "2024-03-04T10:31:40.000Z",
  },
  {
    order_id: 157500,
    preferred: 0,
    stock: {
      id: 15,
      ticker: "DORI",
      issue_code: "UZ7054590003",
      issue_name: "Dori-Darmon",
      currency: "uzs",
      logo: "https://jett.uz/upload/logos/DORI.png",
    },
    repeatable: 0,
    type: "buy-limit",
    market_code: "STK",
    qty: 17,
    price: 10000,
    interest: 2023,
    total: 170000,
    overall: 172023,
    rfb_created_on: null,
    rfb_finished_on: null,
    rfb_error_reason: null,
    status: "processing",
    added_on: "2024-03-04T10:28:30.000Z",
    updated_on: "2024-03-04T10:31:40.000Z",
  },
  {
    order_id: 157499,
    preferred: 0,
    stock: {
      id: 12,
      ticker: "IPKY",
      issue_code: "UZ7039920002",
      issue_name: "Ipak Yo'li Bank",
      currency: "uzs",
      logo: "https://jett.uz/upload/logos/IPKY.png",
    },
    repeatable: 0,
    type: "buy-limit",
    market_code: "STK",
    qty: 100,
    price: 150,
    interest: 178.5,
    total: 15000,
    overall: 15178.5,
    rfb_created_on: null,
    rfb_finished_on: null,
    rfb_error_reason: null,
    status: "processing",
    added_on: "2024-03-04T10:27:49.000Z",
    updated_on: "2024-03-04T10:31:40.000Z",
  },
  {
    order_id: 157498,
    preferred: 0,
    stock: {
      id: 32,
      ticker: "GRBK",
      issue_code: "UZ7037610001",
      issue_name: "GARANT BANK",
      currency: "uzs",
      logo: "https://jett.uz/upload/logos/1668767034.png",
    },
    repeatable: 0,
    type: "buy-limit",
    market_code: "STK",
    qty: 1000,
    price: 200,
    interest: 2380,
    total: 200000,
    overall: 202380,
    rfb_created_on: null,
    rfb_finished_on: null,
    rfb_error_reason: null,
    status: "error",
    added_on: "2024-03-04T10:25:20.000Z",
    updated_on: "2024-03-04T10:26:29.000Z",
  },
  {
    order_id: 157492,
    preferred: 0,
    stock: {
      id: 778,
      ticker: "IFMT3",
      issue_code: "UZ6056967AC7",
      issue_name: "IMKON FINANS",
      currency: "uzs",
      logo: "https://jett.uz/upload/logos/1684491014.svg",
    },
    repeatable: 0,
    type: "sell-market",
    market_code: "BND",
    qty: 1,
    price: 910000,
    interest: 3822,
    total: 910000,
    overall: 906178,
    rfb_created_on: null,
    rfb_finished_on: null,
    rfb_error_reason: null,
    status: "processing",
    added_on: "2024-02-26T12:36:50.000Z",
    updated_on: "2024-03-04T10:26:29.000Z",
  },
  {
    order_id: 157491,
    preferred: 1,
    stock: {
      id: 60,
      ticker: "HMKB1",
      issue_code: "UZ701134K017",
      issue_name: "Hamkorbank",
      currency: "uzs",
      logo: "https://jett.uz/upload/logos/HMKB.png",
    },
    repeatable: 0,
    type: "buy-limit",
    market_code: "STK",
    qty: 23,
    price: 65,
    interest: 17.79,
    total: 1495,
    overall: 1512.79,
    rfb_created_on: null,
    rfb_finished_on: null,
    rfb_error_reason: null,
    status: "approved",
    added_on: "2024-02-26T12:35:28.000Z",
    updated_on: "2024-02-26T12:35:57.000Z",
  },
  {
    order_id: 157490,
    preferred: 0,
    stock: {
      id: 778,
      ticker: "IFMT3",
      issue_code: "UZ6056967AC7",
      issue_name: "IMKON FINANS",
      currency: "uzs",
      logo: "https://jett.uz/upload/logos/1684491014.svg",
    },
    repeatable: 0,
    type: "buy-market",
    market_code: "BND",
    qty: 2,
    price: 1020000,
    interest: 8364,
    total: 2040000,
    overall: 2048364,
    rfb_created_on: null,
    rfb_finished_on: null,
    rfb_error_reason: null,
    status: "approved",
    added_on: "2024-02-26T12:34:47.000Z",
    updated_on: "2024-02-26T12:35:57.000Z",
  },
  {
    order_id: 157489,
    preferred: 1,
    stock: {
      id: 58,
      ticker: "ALK1",
      issue_code: "UZ704476K019",
      issue_name: "Aloqabank",
      currency: "uzs",
      logo: "https://jett.uz/upload/logos/ALKB.png",
    },
    repeatable: 0,
    type: "buy-limit",
    market_code: "STK",
    qty: 10,
    price: 850,
    interest: 101.15,
    total: 8500,
    overall: 8601.15,
    rfb_created_on: null,
    rfb_finished_on: null,
    rfb_error_reason: null,
    status: "approved",
    added_on: "2024-02-26T12:34:28.000Z",
    updated_on: "2024-02-26T12:35:57.000Z",
  },
  {
    order_id: 157488,
    preferred: 1,
    stock: {
      id: 58,
      ticker: "ALK1",
      issue_code: "UZ704476K019",
      issue_name: "Aloqabank",
      currency: "uzs",
      logo: "https://jett.uz/upload/logos/ALKB.png",
    },
    repeatable: 0,
    type: "buy-limit",
    market_code: "STK",
    qty: 11,
    price: 100,
    interest: 13.09,
    total: 1100,
    overall: 1113.09,
    rfb_created_on: null,
    rfb_finished_on: null,
    rfb_error_reason: null,
    status: "approved",
    added_on: "2024-02-26T12:33:45.000Z",
    updated_on: "2024-02-26T12:35:57.000Z",
  },
  {
    order_id: 157487,
    preferred: 0,
    stock: {
      id: 110,
      ticker: "QAPI",
      issue_code: "UZ7001990009",
      issue_name: "Qashqadaryo parmalash ishlari",
      currency: "uzs",
      logo: "https://jett.uz/upload/logos/1692092004.png",
    },
    repeatable: 0,
    type: "buy-market",
    market_code: "STK",
    qty: 11,
    price: 971,
    interest: 127.1,
    total: 10681,
    overall: 10808.1,
    rfb_created_on: null,
    rfb_finished_on: null,
    rfb_error_reason: null,
    status: "approved",
    added_on: "2024-02-26T12:33:23.000Z",
    updated_on: "2024-02-26T12:35:57.000Z",
  },
]);
export default {
  components: {
    Modal,
    Filter,
  },

  data() {
    return {
      userId: 42423314,
      queryFilter: {},

      token:
      "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpZCI6ODYsImFwcF91c2VyX2lkIjoiMTgzMiIsImNsaWVudF9pZCI6NTYsInN0YXR1cyI6Im5ldyIsImFwcF9pZCI6MSwiaWF0IjoxNzEwNzI1NTM2LCJleHAiOjE3MTA4MTE5MzZ9.oG73mkvy9FYzUSCtchiLkSwZYyfV8T1lP0emH3H_loY",
      items: [],
      filterText: "",
      queryFilter: "",
      showModal: false,
      selectedItem: null,
      filterModal: false,
      filter: "./",
    };
  },

  methods: {
    async getData() {
      const url = `https://dev-api.jett.uz${this.$route.href}`;
      const headers = {
        Token: this.token,
        "user-id": this.userId,
      };
      try {
        const response = await fetch(url, { headers });
        const users = await response.json();
        console.log(users);

        this.items = users;
      } catch (error) {
        console.error("Error fetching data:", error);
      }
    },
    formatTimestamp(time) {
      return moment(time).format("HH:mm DD.MM.YYYY");
    },
    handleData(data) {
      this.$router.push({ query: data }); 
      console.log(this.$route.href);
      this.getData();
    },
    openModal(item) {
      this.selectedItem = item;
      this.showModal = true;
    },
    closeModal() {
      this.showModal = false;
      this.selectedItem = null;
    },
    openfilter() {
      this.filterModal = true;
    },
    closeFilter() {
      this.filterModal = false;
    },
  },

  computed: {
    filteredItems() {
      return this.items.filter((item) => {
        return item.stock.issue_name
          .toLowerCase()
          .includes(this.filterText.toLowerCase());
      });
    },
  },
  mounted() {
    this.getData();
  },
};
</script>
<style scoped>
.container {
  width: 100%;
}

.search-box {
  display: flex;
  justify-content: space-between;
  align-items: center;
  width: 100%;
  height: 40px;
  border-radius: 5px;
}
.search-input {
  padding: 0 15px;
  height: 35px;
  border-radius: 10px;
  outline: none;
  border: none;
  width: 100%;
  margin-right: 10px;
  background-color: #e9e5e5;
}

.box {
  display: flex;
  justify-content: space-between;
  align-items: center;
  height: 80px;
  width: 100%;
  border-radius: 15px;
  padding: 15px;
  border: 1px solid rgb(214, 212, 212);
  margin: 10px 0;
  /* box-shadow: rgba(149, 157, 165, 0.2) 0px 8px 24px; */
  cursor: pointer;
}
.box:hover {
  background-color: rgb(243, 243, 242);
}
.logo {
  display: flex;
  padding: 5px;
  justify-content: center;
  align-items: center;
  font-size: 20px;
  margin-right: 10px;
}
.text-container {
  width: 100%;
}
.text-box {
  display: flex;
  width: 100%;
  justify-content: space-between;
}
.logo-img {
  width: 50px;
  height: 50px;
}
.buy {
  font-size: 12px;
  font-weight: 600;
  color: #c4c1c1;
}
.bank-name {
  font-size: 18px;
  color: #5a5959;
  font-weight: 600;
  width: 200px;
  white-space: nowrap;
  text-overflow: ellipsis;
  overflow: hidden;
}
.aksiya {
  font-size: 12px;
  color: rgb(96, 199, 96);
  font-weight: 600;
}
.total {
  font-size: 14px;
  color: red;
  margin: 4px 0 5px;
}
.aksiya-price {
  font-size: 12px;
  color: #000;
}
.status {
  color: rgb(40, 214, 83);
  font-size: 12px;
  font-weight: 600;
}
.canceled {
  color: #e35461 !important;
}
.error {
  color: #8f98a5 !important;
}
.approved {
  color: rgb(19, 192, 19) !important;
}
.processing {
  color: #f79570 !important;
}
</style>
