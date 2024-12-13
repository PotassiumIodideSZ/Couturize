<template>
  <q-dialog v-model="isOpen" persistent maximized>
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

<script>
import { defineComponent } from 'vue'
import { checkAuthAndRedirect } from '../utils/auth'

export default defineComponent({
  name: 'StyleRecommendationModal',
  props: {
    modelValue: {
      type: Boolean,
      default: false
    }
  },
  emits: ['update:modelValue', 'submit'],
  data() {
    return {
      redirectPath: '/',
      season: null,
      style: null,
      price: 0,
      description: ''
    }
  },
  computed: {
    isOpen: {
      get() {
        if (this.modelValue) {
          if (!checkAuthAndRedirect(this.redirectPath)) {
            this.$emit('update:modelValue', false)
            return false
          }
        }
        return this.modelValue
      },
      set(value) {
        this.$emit('update:modelValue', value)
      }
    },
    isFormValid() {
      return this.season && this.style && this.price > 0
    }
  },
  watch: {
    season() { this.checkAuthAndClose() },
    style() { this.checkAuthAndClose() },
    price() { this.checkAuthAndClose() },
    description() { this.checkAuthAndClose() }
  },
  methods: {
    checkAuthAndClose() {
      if (this.modelValue && !checkAuthAndRedirect(this.redirectPath)) {
        this.$emit('update:modelValue', false)
      }
    },
    formatPrice(value) {
      return value ? value.toString().replace(/\B(?=(\d{3})+(?!\d))/g, ' ') + ' ₽' : '0 ₽'
    },
    closeModal() {
      this.$emit('update:modelValue', false)
      this.season = null
      this.style = null
      this.price = 0
      this.description = ''
    },
    onSubmit() {
      if (!checkAuthAndRedirect(this.redirectPath)) return

      this.$emit('submit', {
        season: this.season,
        style: this.style,
        price: this.price,
        description: this.description
      })
      this.closeModal()
    }
  },
  beforeMount() {
    if (this.modelValue && !checkAuthAndRedirect(this.redirectPath)) {
      this.$emit('update:modelValue', false)
    }
  }
})
</script>

<style lang="scss" scoped>
.recommendation-modal {
  width: 90%;
  max-width: 800px;
  margin: auto;
  border-radius: 8px;
  background: var(--color-primary-bg);
  color: var(--text-color);

  .modal-header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 16px;
    border-bottom: 1px solid var(--highlight-color);
  }

  :deep(.q-slider__selection) {
    background: var(--highlight-color);
  }

  :deep(.q-slider__thumb) {
    color: var(--highlight-color);
  }
}
</style>
