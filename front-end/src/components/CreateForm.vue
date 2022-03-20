<script>
import {
  NSpace, NGrid, NGi,
  NForm, NFormItem, NRadioGroup, NRadioButton,
  NButton, NInput
} from 'naive-ui'

export default {
  components: {
    NSpace,
    NGrid,
    NGi,
    NForm,
    NFormItem,
    NRadioGroup,
    NRadioButton,
    NButton,
    NInput
  },
  data () {
    return {
      dok: {
        method: 'smart-id',
        pealkiri: '',
        sisu: ''
      },
      handleSignButtonClick (dok) {
        console.log(JSON.stringify(dok, null, 2))
      }
    }
  }
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
            show-require-mark
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
            show-require-mark
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
              label="Isikukood"
              path="dok.isikukood"
              :show-require-mark="dok.method === 'smart-id' || dok.method === 'id-card'"
            >
              <n-input
                v-model:value="dok.isikukood"
                type="text"
                placeholder="Isikukood"
                :disabled="dok.method === 'mobile-id'"
              />
            </n-form-item>
            <n-form-item
              label="Telefon"
              path="dok.telefon"
              :show-require-mark="dok.method === 'mobile-id'"
            >
              <n-input
                v-model:value="dok.telefon"
                type="text"
                placeholder="Telefon"
                :disabled="dok.method === 'smart-id' || dok.method === 'id-card'"
                hidden="true"
              />
            </n-form-item>
            <n-form-item
              label="Vali allkirjastusmeetod"
              path="dok.telefon"
              show-require-mark
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
          </n-space>
          <n-button
            :disabled="dok.pealkiri === '' || dok.sisu === ''"
            round
            type="primary"
            value="mid"
            @click="handleSignButtonClick(dok)"
          >
            Allkirjasta
          </n-button>
        </n-space>
      </n-form>
      <pre>{{ JSON.stringify(dok, null, 2) }}</pre>
    </n-gi>
  </n-grid>
</template>
