<script setup>
import { ref } from "vue";
const Jobs = ref([]);
const newJobName = ref("");
const newJobState = ref(0);

const addJob = () => {
  if (newJobName.value != "") {
    Jobs.value.push({
      name: newJobName.value,
      state: newJobState.value,
    });
    newJobName.value = "";
    newJobState.value = 0;
  }
};

const finishJob = (job) => {
  job.state = 1;
};

const deleteJob = (job) => {
  job.state = -1;
};
</script>

<template>
  <div>ToDoList</div>
  <div v-for="job in Jobs" :key="job.name">
    <div v-if="job.state != -1" class="job">
      <div v-if="job.state == 0">
        <div class="name">名前:{{ job.name }}</div>
        頑張ろう！<button @click="finishJob(job)">finish!</button>
      </div>
    </div>
  </div>
  <div>------終わった------</div>
  <div v-for="job in Jobs" :key="job.name">
    <div v-if="job.state != -1" class="job">
      <div v-if="job.state == 1">
        <div class="name">名前:{{ job.name }}</div>
        お疲れ様！<button @click="deleteJob(job)">Delete!</button>
      </div>
    </div>
  </div>
  <div>
    <label>
      名前
      <input v-model="newJobName" type="text" />
    </label>
    <button @click="addJob">add</button>
  </div>
</template>

<style></style>
