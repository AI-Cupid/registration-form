<template>
  <div class="row justify-between q-col-gutter-y-md q-col-gutter-x-sm">
    <q-input
      v-model="entity.phone_number"
      class="col-12"
      mask="(###) ###-####"
      :label="$t('phoneNumber')"
      dense
    />
    <q-input
      v-model="entity.first_name"
      class="col-6"
      :label="$t('firstName')"
      dense
    />
    <q-input
      v-model="entity.last_name"
      class="col-6"
      :label="$t('lastName')"
      dense
    />
    <q-select
      v-model="entity.age"
      :options="ageOptions"
      class="col-6"
      :label="$t('age')"
      dense
    />
    <q-select
      v-model="entity.gender"
      :options="getGenderOptions()"
      emit-value
      map-options
      option-value="id"
      option-label="label"
      class="col-6"
      :label="$t('gender')"
      dense
    />
    <q-input
      v-model="entity.bio"
      class="col-12"
      :label="$t('bio')"
      type="textarea"
      dense
      autogrow
    />
    <q-btn
      :label="$t('submit')"
      class="col q-py-xs q-mt-md q-mx-lg"
      @click="handleSubmit"
      color="primary"
      noCaps
    />
  </div>
</template>

<script setup lang="ts">
import { useI18n } from 'vue-i18n';
import { ref } from 'vue';
import { createClient } from '@supabase/supabase-js';

interface IUser {
  phone_number: string;
  first_name: string;
  last_name: string;
  age: string;
  gender: string;
  bio: string;
}

const supabaseUrl = 'https://vhfymgdmtvjpitnlruuq.supabase.co';
const supabaseKey =
  'eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJzdXBhYmFzZSIsInJlZiI6InZoZnltZ2RtdHZqcGl0bmxydXVxIiwicm9sZSI6ImFub24iLCJpYXQiOjE2OTYyMDY0ODMsImV4cCI6MjAxMTc4MjQ4M30.rtFqHXabezswjJydQTYembdjoRa8Il1QKBYH71VQtOw';
const supabase = createClient(supabaseUrl, supabaseKey);

const { t } = useI18n({ useScope: 'global' });
const entity = ref<IUser>({
  phone_number: '',
  first_name: '',
  last_name: '',
  age: '',
  gender: '',
  bio: '',
});
const genderOptions = [
  { id: 'cb267d3f-ac75-4a07-99fa-40f2c2e5b91f', label: 'male' },
  { id: '2465f2f8-389d-40ce-b2d8-111298eb2b68', label: 'female' },
];

const ageOptions: number[] = [];
for (let i = 18; i < 100; i++) ageOptions.push(i);

const getGenderOptions = () => {
  const translatedOptions = [];
  for (let i = 0; i < genderOptions.length; i++) {
    const option = genderOptions[i];
    const translatedOption = { id: option.id, label: t(option.label) };
    translatedOptions.push(translatedOption);
  }
  return translatedOptions;
};

const handleSubmit = async () => {
  await supabase.from('USERS').insert([entity.value]);
};
</script>
