<script setup>
import banner from "@/assets/banner.png";
import InfoCard from "@/components/InfoCard.vue";
import { ref } from "vue";

import { initializeApp } from "firebase/app";
import { getFirestore, collection, getDocs } from "firebase/firestore";

const isLoading = ref(true);
const db = getFirestore(initializeApp);
const docRef = collection(db, "Diary");
const mydiary = ref([]);
const getCollections = (docRef) => {
  return new Promise((resolve, reject) => {
    getDocs(docRef)
      .then((collections) => {
        collections.docs.forEach((val) => {
          mydiary.value.push(val.data());
        });
        isLoading.value = false;
        resolve(collections.docs);
      })
      .catch((err) => {
        isLoading.value = true;
        alert(err.message);
      }),
      reject;
  });
};
getCollections(docRef);
</script>

<template>
  <main>
    <div class="container">
      <img class="web-banner" :src="banner" alt="" />

      <div class="my-3">
        <div class="row">
          <div class="col-md-3">
            <RouterLink to="/add" class="btn btn-primary w-100" type="button"
              >เพิ่มรายการ</RouterLink
            >
          </div>
        </div>
      </div>

      <div class="row gy-2">
        <h4 v-if="isLoading">กำลังโหลด...</h4>
        <InfoCard
          :title="stmt.title"
          :price="stmt.price"
          :description="stmt.description"
          :time="stmt.time"
          :isIncome="stmt.isIncome"
          v-for="(stmt, i) in mydiary"
          :key="i"
        />
      </div>
    </div>
  </main>
</template>

<style scoped>
.web-banner {
  width: 100%;
}
</style>
