<script>
import {
  NSpace, NGrid, NGi,
  NRadioGroup, NRadioButton,
  NButton, NInput
} from 'naive-ui'

export default {
  components: {
    NSpace,
    NGrid,
    NGi,
    NRadioGroup,
    NRadioButton,
    NButton,
    NInput
  },
  data () {
    return {
      method: 'smart-id'
    }
  }
}

</script>

<template>
  <n-grid cols="4">
    <n-gi span="4">
      <n-space vertical>
        Selected method {{ method }}.
        <n-input
          v-model:value="pealkiri"
          type="text"
          placeholder="Pealkiri"
        />
        <n-input
          v-model:value="sisu"
          type="textarea"
          placeholder="Sisu"
          rows="5"
        />

        <n-space horizontal>
          <n-input
            v-model:value="isikukood"
            type="text"
            placeholder="Isikukood"
          />
          <n-input
            v-model:value="telefon"
            type="text"
            placeholder="Telefon"
            hidden="true"
          />
          <n-radio-group
            v-model:value="method"
            name="method"
            style="margin-bottom: 12px"
          >
            <n-radio-button value="mobile-id">
              Mobiil-ID
            </n-radio-button>
            <n-radio-button value="smart-id">
              Smart-ID
            </n-radio-button>
            <n-radio-button value="id-card">
              ID kaart
            </n-radio-button>
          </n-radio-group>
          <n-button
            round
            strong
            primary
            value="mid"
          >
            Allkirjasta
          </n-button>
        </n-space>
      </n-space>
    </n-gi>
  </n-grid>
</template>
