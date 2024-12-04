<template>
  <q-dialog v-model="isOpen" persistent>
    <q-card class="recommendation-modal">
      <div class="modal-header">
        <div class="text-h5">Создание новой рекомендации</div>
        <q-btn flat round icon="close" @click="closeModal" />
      </div>

      <q-card-section>
        <div class="row q-col-gutter-md">
          <!-- Сезон -->
          <div class="col-12 col-sm-6">
            <div class="text-subtitle1 q-mb-sm">Выберите сезон:</div>
            <div class="q-gutter-y-sm">
              <q-radio v-model="season" val="winter" label="Зима" />
              <q-radio v-model="season" val="spring" label="Весна" />
              <q-radio v-model="season" val="summer" label="Лето" />
              <q-radio v-model="season" val="autumn" label="Осень" />
            </div>
          </div>

          <!-- Стиль -->
          <div class="col-12 col-sm-6">
            <div class="text-subtitle1 q-mb-sm">Выберите стиль:</div>
            <div class="q-gutter-y-sm">
              <q-radio v-model="style" val="business" label="Деловой" />
              <q-radio v-model="style" val="sport" label="Спортивный" />
              <q-radio v-model="style" val="casual" label="Кэжуал" />
              <q-radio v-model="style" val="underwear" label="Бельевой" />
              <q-radio v-model="style" val="outerwear" label="Верхняя одежда" />
            </div>
          </div>
        </div>

        <!-- Стоимость -->
        <div class="q-mt-lg">
          <div class="text-subtitle1 q-mb-sm">Стоимость, руб</div>
          <q-slider
            v-model="price"
            :min="0"
            :max="1000000"
            :step="1000"
            label
            label-always
            color="primary"
          >
            <template v-slot:thumb-label>
              {{ formatPrice(price) }}
            </template>
          </q-slider>
        </div>
      </q-card-section>

      <q-card-actions align="center" class="q-pa-md">
        <q-btn
          label="ДАЛЕЕ"
          color="primary"
          class="full-width"
          :disable="!isFormValid"
          @click="onSubmit"
        />
      </q-card-actions>
    </q-card>
  </q-dialog>
</template>

<script setup>
import { ref, computed } from 'vue'

const props = defineProps({
  modelValue: {
    type: Boolean,
    default: false
  }
})

const emit = defineEmits(['update:modelValue', 'submit'])

const isOpen = computed({
  get: () => props.modelValue,
  set: (value) => emit('update:modelValue', value)
})

const season = ref(null)
const style = ref(null)
const price = ref(0)

const isFormValid = computed(() => {
  return season.value && style.value && price.value > 0
})

const formatPrice = (value) => {
  return new Intl.NumberFormat('ru-RU').format(value)
}

const closeModal = () => {
  isOpen.value = false
}

const onSubmit = () => {
  emit('submit', {
    season: season.value,
    style: style.value,
    price: price.value
  })
  closeModal()
}
</script>

<style lang="scss" scoped>
.recommendation-modal {
  width: 100%;
  max-width: 600px;
  background: var(--dark-page);
}

.modal-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 20px;
  border-bottom: 1px solid rgba(255, 255, 255, 0.1);
}

:deep(.q-slider) {
  &__selection {
    background: var(--q-primary);
  }
  
  &__thumb {
    background: var(--q-primary);
  }
}
</style>
