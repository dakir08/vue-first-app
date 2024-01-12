<script setup lang="ts">
import { computed, PropType } from "vue";
import { Job } from "../models/Job";
import { OrderTerm } from "../models/OrderTerm";

const props = defineProps({
  jobs: {
    required: true,
    type: Array<Job>
  },
  order: {
    required: true,
    type: String as PropType<OrderTerm>
  }
});

const orderedJobs = computed(() => {
  return [...props.jobs].sort((a, b) => {
    return a[props.order] > b[props.order] ? 1 : -1;
  });
});

console.log("?orderedJobs", orderedJobs);
console.log("?order", props.order);
</script>

<template>
  <div class="job-list">
    <transition-group name="list" tag="ul">
      <li v-for="job in orderedJobs" :key="job.id">
        <h2>{{ job.title }} in {{ job.location }}</h2>
        <div class="salary">
          <img src="../assets/rupee.svg" alt="Rupee Image" />
          <p>{{ job.salary }} rupees</p>
        </div>
        <div class="description">Bla bla bla</div>
      </li>
    </transition-group>
  </div>
</template>

<style scoped>
.job-list {
  max-width: 960px;
  margin: 40px auto;
}
.job-list ul {
  padding: 0;
}
.job-list li {
  list-style-type: none;
  background: white;
  padding: 16px;
  margin: 16px 0;
  border-radius: 4px;
}
.job-list h2 {
  margin: 0 0 10px;
  text-transform: capitalize;
}
.salary {
  display: flex;
}
.salary img {
  width: 30px;
}
.salary p {
  color: #17bf66;
  font-weight: bold;
  margin: 10px 4px;
}

.list-move {
  transition: all 1s;
}
</style>
