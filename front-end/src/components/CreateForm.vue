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

function handleSignButtonClick (params) {
  console.log(JSON.stringify(params, null, 2))
  const form = document.createElement('form')
  form.method = 'POST'
  form.action = '/sign'

  for (const key in params) {
    if (params.hasOwnProperty(key)) {
      const hiddenField = document.createElement('input')
      hiddenField.type = 'hidden'
      hiddenField.name = key
      hiddenField.value = params[key]

      form.appendChild(hiddenField)
    }
  }

  document.body.appendChild(form)
  form.submit()
}

</script>

<template>
  <n-grid cols="4">
    <n-gi span="4">
      <n-form
        ref="formRef"
        inline
        :label-width="80"
        :model="dok"
      >
        <n-space vertical>
          <n-form-item
            label="Pealkiri"
            path="dok.pealkiri"
          >
            <n-input
              v-model:value="dok.pealkiri"
              type="text"
              placeholder="Pealkiri"
              @keydown.enter.prevent
            />
          </n-form-item>
          <n-form-item
            label="Sisu"
            path="dok.sisu"
          >
            <n-input
              v-model:value="dok.sisu"
              type="textarea"
              placeholder="Sisu"
              rows="5"
            />
          </n-form-item>

          <n-space horizontal>
            <n-form-item
              label="Vali allkirjastusmeetod"
              path="dok.telefon"
            >
              <n-radio-group
                v-model:value="dok.method"
                name="method"
                style="margin-bottom: 12px"
              >
                <n-radio-button value="id-card">
                  ID kaart
                </n-radio-button>
                <n-radio-button value="mobile-id">
                  Mobiil-ID
                </n-radio-button>
                <n-radio-button value="smart-id">
                  Smart-ID
                </n-radio-button>
              </n-radio-group>
            </n-form-item>
            <div v-show="dok.method === 'mobile-id'">
              <n-form-item
                label="Telefon"
                path="dok.telefon"
              >
                <n-input
                  v-model:value="dok.telefon"
                  type="text"
                  placeholder="Telefon"
                />
              </n-form-item>
            </div>
            <div v-show="dok.method === 'smart-id'">
              <n-form-item
                label="Isikukood"
                path="dok.isikukood"
              >
                <n-input
                  v-model:value="dok.isikukood"
                  type="text"
                  placeholder="Isikukood"
                />
              </n-form-item>
            </div>
          </n-space>
          <n-button
            :disabled="dok.pealkiri === ''
              || dok.sisu === ''"
            round
            type="primary"
            value="mid"
            @click="handleSignButtonClick(dok)"
          >
            Allkirjasta
          </n-button>
        </n-space>
      </n-form>
    </n-gi>
  </n-grid>
</template>
