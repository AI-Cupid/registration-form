<template>
  <div class="row justify-between q-gutter-y-sm">
    <q-input
      v-model="entity.phoneNumber"
      class="q-px-xs col-12"
      mask="(###) ###-####"
      :label="$t('phoneNumber')"
      dense
    />
    <q-input
      v-model="entity.firstName"
      class="q-px-xs col-6"
      :label="$t('firstName')"
      dense
    />
    <q-input
      v-model="entity.lastName"
      class="q-px-xs col-6"
      :label="$t('lastName')"
      dense
    />
    <q-select
      v-model="entity.age"
      :options="ageOptions"
      class="q-px-xs col-6"
      :label="$t('age')"
      dense
    />
    <q-select
      v-model="entity.gender"
      :options="getGenderOptions()"
      class="q-px-xs col-6"
      :label="$t('gender')"
      dense
    />
    <q-input
      v-model="entity.bio"
      class="q-px-xs col-12"
      :label="$t('bio')"
      type="textarea"
      dense
    />
  </div>
</template>

<script setup lang="ts">
import { useI18n } from 'vue-i18n';
import { ref } from 'vue';

const { t } = useI18n({ useScope: 'global' });
const entity = ref({});
const genderOptions = [
  { id: 1, label: 'male' },
  { id: 2, label: 'female' },
];

const ageOptions: number[] = []
for (let i = 18; i < 100; i++)
  ageOptions.push(i)

const getGenderOptions = () => {
  const translatedOptions = []
  for (let i = 0; i < genderOptions.length; i++) {
    const option = genderOptions[i]
    const translatedOption = { id: option.id, label: t(option.label) }
    translatedOptions.push(translatedOption)
  }
  return translatedOptions
}
</script>
