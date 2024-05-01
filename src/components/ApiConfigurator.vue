<template>
  <div>
    <h3>API Configuration</h3>
    <v-text-field v-model="apiUrl" label="API URL" outlined></v-text-field>
    <v-select
      v-model="apiMethod"
      :items="['GET', 'POST', 'PUT', 'DELETE']"
      label="API Method"
      outlined
    ></v-select>
    <v-textarea
      v-model="requestHeaders"
      label="Request Headers"
      outlined
    ></v-textarea>
    <v-textarea
      v-model="queryParams"
      label="Query Parameters"
      outlined
    ></v-textarea>
    <v-textarea v-model="requestBody" label="Request Body" outlined></v-textarea>
    <v-btn color="primary" @click="addAPIConfig">Add API Config</v-btn>
  </div>
</template>

<script setup>
import { ref } from 'vue'

const apiUrl = ref('')
const apiMethod = ref('GET')
const requestHeaders = ref('')
const queryParams = ref('')
const requestBody = ref('')

const emit = defineEmits(['apiConfigAdded'])

const addAPIConfig = () => {
  const apiConfig = {
    url: apiUrl.value,
    method: apiMethod.value,
    headers: parseJSON(requestHeaders.value),
    params: parseJSON(queryParams.value),
    data: parseJSON(requestBody.value),
  }
  emit('apiConfigAdded', apiConfig)
  resetFields()
}

const parseJSON = (str) => {
  try {
    return JSON.parse(str)
  } catch (e) {
    return {}
  }
}

const resetFields = () => {
  apiUrl.value = ''
  apiMethod.value = 'GET'
  requestHeaders.value = ''
  queryParams.value = ''
  requestBody.value = ''
}
</script>
