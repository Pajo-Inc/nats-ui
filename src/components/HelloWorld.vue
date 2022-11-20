<script setup lang="ts">
import {onMounted, reactive, ref} from 'vue'
import jsonp from 'jsonp'

defineProps<{ msg: string }>()

const fetchVarz = () => {
  jsonp("http://localhost:8222/varz", null, (err, data) => {
    if (err) {
      console.error(err.message);
    } else {
      console.log(data);
      varz.value = data;
    }
  });
};

const fetchAccountz = () => {
  jsonp("http://localhost:8222/accountz", null, (err, data) => {
    if (err) {
      console.error(err.message);
    } else {
      console.log(data);
      accountz.value = data;
    }
  });
};

const fetchJetsreamz = () => {
  jsonp("http://localhost:8222/jsz", null, (err, data) => {
    if (err) {
      console.error(err.message);
    } else {
      console.log(data);
      jsz.value = data;
    }
  });
};

onMounted(() => {
  fetchVarz()
  fetchAccountz()
  fetchJetsreamz()
})

const count = ref(0)
const varz = ref({})
const accountz = ref({})
const jsz = ref({})
</script>

<template>
  <h1>{{ msg }}</h1>
  <h2>Varz</h2>
  <div v-for="(value, name) in varz">
    {{ name }}: {{ value }}
  </div>
  <h2>Accountz</h2>
  <div v-for="(value, name) in accountz">
    {{ name }}: {{ value }}
  </div>
  <h2>Jetstreamz</h2>
  <div v-for="(value, name) in jsz">
    {{ name }}: {{ value }}
  </div>
</template>

<style scoped>
.read-the-docs {
  color: #888;
}
</style>
