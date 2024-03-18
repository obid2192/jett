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
  width: 100%;
  border-radius: 15px;
  padding: 5px 10px;
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
