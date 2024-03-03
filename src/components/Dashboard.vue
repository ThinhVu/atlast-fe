<template>
  <section data-name="dashboard" class="dashboard fc w-100 h-100 fg-12px py-3 px-3 ovf-y-s hide-scroll-bar">
    <section data-name="metric" class="fr ai-c jc-sb fg-8px">
      <div class="f1 metric-block bc-r-0">
        <p class="label c-r-4">Users</p>
        <p class="val c-r-7">{{ appMetric.user }}</p>
      </div>
    </section>
  </section>
</template>
<script setup>
import {onBeforeUnmount, onMounted, ref} from 'vue'
import {systemAPI} from '@/api';

const appMetric = ref({
  user: 0
})

function loadAppMetric() {
  systemAPI.getAppMetric().then(resp => appMetric.value = resp)
}

let interval;
onMounted(() => {
  loadAppMetric()
  interval = setInterval(loadAppMetric, 10000)
})
onBeforeUnmount(() => {
  clearInterval(interval)
})
</script>
<style scoped>
.dashboard {
}

.metric-block {
  border: 1px solid rgb(216, 222, 228);
  box-shadow: 0 3px 6px rgba(140,149,159,0.15);
  border-radius: 10px;
  padding: 20px;
  color: #676b79;
}

.metric-block .label {
  font-size: 12px;
  color: #adaeaf;
}

.metric-block  .val {
  font-size: 30px;
}
</style>
