<script setup lang="ts">
import { reactive } from 'vue'
import { useI18n } from 'vue-i18n'
import { ElSpace, ElCard, ElRow, ElCol, ElForm, ElFormItem, ElInput, ElInputNumber, ElSelect, ElOption, ElDatePicker, ElTimePicker, ElRadioGroup, ElRadio, ElSwitch, ElCheckboxGroup, ElCheckbox, ElRate, ElColorPicker, ElSlider } from 'element-plus'

const i18n = useI18n()

const form = reactive({
  name: '',
  sex: '',
  age: 0,
  region: '',
  date: '',
  time: '',
  rate: 0,
  score: 0,
  choice: [],
  private: false,
  color: '',
  note: '',
})
</script>

<template>
  <el-space direction="vertical" fill size="large" class="px-80 py-4 w-full">
    <el-card shadow="always">
      <el-form :model="form">
        <el-form-item :label="i18n.t('form.basic.name')">
          <el-input v-model="form.name" name="name" :label="i18n.t('form.basic.name')" :placeholder="i18n.t('form.basic.name_placeholder')" clearable />
        </el-form-item>

        <el-form-item :label="i18n.t('form.basic.sex')">
          <el-radio-group v-model="form.sex" name="sex" :label="i18n.t('form.basic.sex')">
            <el-radio :label="i18n.t('form.basic.sex_male')" name="male" border />
            <el-radio :label="i18n.t('form.basic.sex_female')" name="female" border />
          </el-radio-group>
        </el-form-item>

        <el-form-item :label="i18n.t('form.basic.age')">
          <el-input-number v-model="form.age" name="age" :label="i18n.t('form.basic.age')" :placeholder="i18n.t('form.basic.age_placeholder')" :min="0" :max="150" :step="1" step-strictly />
        </el-form-item>

        <el-form-item :label="i18n.t('form.basic.area')">
          <el-select v-model="form.region" name="area" :placeholder="i18n.t('form.basic.area_placeholder')" clearable>
            <el-option :label="i18n.t('form.basic.area_beijing')" value="beijing" />
            <el-option :label="i18n.t('form.basic.area_shanghai')" value="shanghai" />
          </el-select>
        </el-form-item>

        <el-form-item :label="i18n.t('form.basic.date_time')">
          <el-row>
            <el-col :span="11">
              <el-date-picker v-model="form.date" :name="i18n.t('form.basic.date')" :placeholder="i18n.t('form.basic.date_placeholder')" />
            </el-col>
            <el-col :span="2" class="text-center">
              <span class="text-gray-500">-</span>
            </el-col>
            <el-col :span="11">
              <el-time-picker v-model="form.time" :name="i18n.t('form.basic.time')" :placeholder="i18n.t('form.basic.time_placeholder')" />
            </el-col>
          </el-row>
        </el-form-item>

        <el-form-item :label="i18n.t('form.basic.rate')">
          <el-rate v-model="form.rate" :colors="['#99A9BF', '#F7BA2A', '#FF9900']" allow-half clearable :label="i18n.t('form.basic.rate')" />
        </el-form-item>

        <el-form-item :label="i18n.t('form.basic.score')">
          <el-slider v-model="form.score" :label="i18n.t('form.basic.score')" show-input show-input-controls show-stops show-tooltip />
        </el-form-item>

        <el-form-item :label="i18n.t('form.basic.choice')">
          <el-checkbox-group v-model="form.choice" :label="i18n.t('form.basic.choice')">
            <el-checkbox :label="i18n.t('form.basic.choice_service')" name="service" border />
            <el-checkbox :label="i18n.t('form.basic.choice_device')" name="device" border />
            <el-checkbox :label="i18n.t('form.basic.choice_environment')" name="environment" border />
          </el-checkbox-group>
        </el-form-item>

        <el-form-item :label="i18n.t('form.basic.private')">
          <el-switch v-model="form.private" name="private" />
        </el-form-item>

        <el-form-item :label="i18n.t('form.basic.color')">
          <el-color-picker v-model="form.color" name="color" :label="i18n.t('form.basic.color')" show-alpha />
        </el-form-item>

        <el-form-item :label="i18n.t('form.basic.note')">
          <el-input v-model="form.note" type="textarea" name="name" :label="i18n.t('form.basic.note')" :placeholder="i18n.t('form.basic.note_placeholder')" show-word-limit />
        </el-form-item>
      </el-form>
    </el-card>
  </el-space>
</template>

<style scoped lang="scss"></style>
