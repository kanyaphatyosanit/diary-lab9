<template>
  <div class="col-md-6">
    <div class="card h-100">
      <div class="card-header d-flex justify-content-between border-bottom-0 bg-dark text-light">
        <h5 class="m-0">;วันที่ {{ dayjs(props.time).format("DD/MM/YYYY") }}</h5>
      </div>
      <div class="card-body">
        <h4 v-if="props.title">{{ props.title }}</h4>

        <p>{{ props.description }}</p>
      </div>
    </div>
  </div>
</template>
<script setup>
import { defineProps } from "vue";
import dayjs from "dayjs";
const props = defineProps({
  title: String,
  description: String,
  time: String
});
</script>
