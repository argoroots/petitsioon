<script setup>
// This starter template is using Vue 3 <script setup> SFCs
// Check out https://v3.vuejs.org/api/sfc-script-setup.html#sfc-script-setup
// import HelloWorld from './components/HelloWorld.vue'
import { NGrid, NGi, NButtonGroup, NButton, NInput } from 'naive-ui'

</script>

<template>
  <n-form
    ref="formRef"
    :model="model"
    :rules="rules"
    :size="size"
    label-placement="top"
  >
    <n-grid
      :span="24"
      :x-gap="24"
    >
      <n-form-item-gi
        :span="12"
        label="Input"
        path="inputValue"
      >
        <n-input
          v-model:value="model.inputValue"
          placeholder="Input"
        />
      </n-form-item-gi>
      <n-form-item-gi
        :span="12"
        label="Textarea"
        path="textareaValue"
      >
        <n-input
          v-model:value="model.textareaValue"
          placeholder="Textarea"
          type="textarea"
          :autosize="{
            minRows: 3,
            maxRows: 5
          }"
        />
      </n-form-item-gi>
      <n-form-item-gi
        :span="12"
        label="Select"
        path="selectValue"
      >
        <n-select
          v-model:value="model.selectValue"
          placeholder="Select"
          :options="generalOptions"
        />
      </n-form-item-gi>
      <n-form-item-gi
        :span="12"
        label="Multiple Select"
        path="multipleSelectValue"
      >
        <n-select
          v-model:value="model.multipleSelectValue"
          placeholder="Select"
          :options="generalOptions"
          multiple
        />
      </n-form-item-gi>
      <n-form-item-gi
        :span="12"
        label="Datetime"
        path="datetimeValue"
      >
        <n-date-picker
          v-model:value="model.datetimeValue"
          type="datetime"
        />
      </n-form-item-gi>
      <n-form-item-gi
        :span="12"
        label="Switch"
        path="switchValue"
      >
        <n-switch v-model:value="model.switchValue" />
      </n-form-item-gi>
      <n-form-item-gi
        :span="12"
        label="Checkbox Group"
        path="checkboxGroupValue"
      >
        <n-checkbox-group v-model:value="model.checkboxGroupValue">
          <n-space>
            <n-checkbox value="Option 1">
              Option 1
            </n-checkbox>
            <n-checkbox value="Option 2">
              Option 2
            </n-checkbox>
            <n-checkbox value="Option 3">
              Option 3
            </n-checkbox>
          </n-space>
        </n-checkbox-group>
      </n-form-item-gi>
      <n-form-item-gi
        :span="12"
        label="Radio Group"
        path="radioGroupValue"
      >
        <n-radio-group
          v-model:value="model.radioGroupValue"
          name="radiogroup1"
        >
          <n-space>
            <n-radio value="Radio 1">
              Radio 1
            </n-radio>
            <n-radio value="Radio 2">
              Radio 2
            </n-radio>
            <n-radio value="Radio 3">
              Radio 3
            </n-radio>
          </n-space>
        </n-radio-group>
      </n-form-item-gi>
      <n-form-item-gi
        :span="12"
        label="Radio Button Group"
        path="radioGroupValue"
      >
        <n-radio-group
          v-model:value="model.radioGroupValue"
          name="radiogroup2"
        >
          <n-radio-button value="Radio 1">
            Radio 1
          </n-radio-button>
          <n-radio-button value="Radio 2">
            Radio 2
          </n-radio-button>
          <n-radio-button value="Radio 3">
            Radio 3
          </n-radio-button>
        </n-radio-group>
      </n-form-item-gi>
      <n-form-item-gi
        :span="12"
        label="Input Number"
        path="inputNumberValue"
      >
        <n-input-number v-model:value="model.inputNumberValue" />
      </n-form-item-gi>
      <n-form-item-gi
        :span="12"
        label="Time Picker"
        path="timePickerValue"
      >
        <n-time-picker v-model:value="model.timePickerValue" />
      </n-form-item-gi>
      <n-form-item-gi
        :span="12"
        label="Slider"
        path="sliderValue"
      >
        <n-slider
          v-model:value="model.sliderValue"
          :step="5"
        />
      </n-form-item-gi>
      <n-form-item-gi
        :span="14"
        label="Transfer"
        path="transferValue"
      >
        <n-transfer
          v-model:value="model.transferValue"
          style="width: 100%"
          :options="generalOptions"
        />
      </n-form-item-gi>
      <n-form-item-gi
        :span="5"
        label="Nested Path"
        path="nestedValue.path1"
      >
        <n-cascader
          v-model:value="model.nestedValue.path1"
          placeholder="Nested Path 1"
          :options="cascaderOptions"
        />
      </n-form-item-gi>
      <n-form-item-gi
        :span="5"
        path="nestedValue.path2"
      >
        <n-select
          v-model:value="model.nestedValue.path2"
          placeholder="Nested Path 2"
          :options="generalOptions"
        />
      </n-form-item-gi>
      <n-gi :span="24">
        <div style="display: flex; justify-content: flex-end">
          <n-button
            round
            type="primary"
            @click="handleValidateButtonClick"
          >
            Validate
          </n-button>
        </div>
      </n-gi>
    </n-grid>
  </n-form>

  <n-grid
    x-gap="12"
    cols="3"
    item-responsive
    responsive="screen"
  >
    <n-gi span="2">
      <div class="light-green">
        <n-input
          v-model:value="value"
          type="text"
          placeholder="Pealkiri"
        />
        <n-input
          v-model:value="value"
          type="textarea"
          placeholder="Sisu"
        />
      </div>
    </n-gi>
    <n-gi>
      <div class="green">
        <n-button-group
          vertical
          size="large"
        >
          <n-button type="primary">
            Mobile-ID
          </n-button>
          <n-button type="primary">
            Smart-ID
          </n-button>
          <n-button type="primary">
            ID-Card
          </n-button>
        </n-button-group>
      </div>
    </n-gi>
  </n-grid>
</template>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
