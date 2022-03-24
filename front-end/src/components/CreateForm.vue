<script setup>
import { ref } from 'vue'

import {
  NSpace, NGrid, NGi,
  NForm, NFormItem, NRadioGroup, NRadioButton,
  NButton, NInput
} from 'naive-ui'

console.log('hello script setup')

const dok = ref({
  method: 'smart-id',
  pealkiri: '',
  sisu: ''
})

async function handleSignButtonClick () {
  console.log(dok.value)
  fetch(import.meta.env.VITE_APP_API_URL, {
    method: 'POST',
    mode: 'no-cors', // no-cors, *cors, same-origin
    body: '{}'
  }).then(resp => {
    console.log('FOO')
    console.table(resp)
  })
}

</script>

<template>
  <n-form
    ref="formRef"
    inline
    :label-width="80"
    :model="dok"
  >
    <n-space vertical>
      <n-form-item
        label="Pealkiri"
        path="pealkiri"
      >
        <n-input
          v-model:value="dok.pealkiri"
          type="text"
          placeholder=""
        />
      </n-form-item>
      <n-form-item
        label="Sisu"
        path="sisu"
      >
        <n-input
          v-model:value="dok.sisu"
          type="textarea"
          placeholder=""
          rows="5"
        />
      </n-form-item>

      <n-space horizontal>
        <n-form-item label="Allkirjastusmeetod">
          <n-radio-group
            v-model:value="dok.method"
            name="method"
          >
            <n-radio-button value="id-card">
              ID kaart
            </n-radio-button>
            <n-radio-button value="smart-id">
              Smart-ID
            </n-radio-button>
            <n-radio-button value="mobile-id">
              Mobiil-ID
            </n-radio-button>
          </n-radio-group>
        </n-form-item>
        <div v-show="dok.method === 'smart-id' || dok.method === 'mobile-id'">
          <n-form-item
            label="Isikukood"
            path="isikukood"
          >
            <n-input
              v-model:value="dok.isikukood"
              type="text"
              placeholder=""
            />
          </n-form-item>
        </div>
        <div v-show="dok.method === 'mobile-id'">
          <n-form-item
            label="Telefon"
            path="telefon"
          >
            <n-input
              v-model:value="dok.telefon"
              type="text"
              placeholder=""
            />
          </n-form-item>
        </div>
      </n-space>
      <n-button
        :disabled="dok.pealkiri === ''
          || dok.sisu === ''
          || (dok.method === 'smart-id'
            && (dok.isikukood === undefined
              || !dok.isikukood.match('^[0-9]{11}$')))
          || (dok.method === 'mobile-id'
            && (dok.telefon === undefined
              || !dok.telefon.match('^[0-9 (+)]{7,}$')))"
        round
        type="primary"
        value="mid"
        @click="handleSignButtonClick()"
      >
        Allkirjasta
      </n-button>
    </n-space>
  </n-form>
</template>

<style scoped>
  .n-form {
    margin: 3rem auto;
    max-width: 40rem;
    width: 90%;
    display: block;
  }
</style>
