<template>
  <q-page class="flex flex-center page-main">
    <section class="banner-section section">
      <img src="../assets/HeroBanner.png" alt="Banner" style="width: 100%;" />
    </section>
    <div class="main-page-container">
      <div class="section title-text" id="section1">
        <div class="style-title"><span class="highlight">ВАШ</span> СТИЛЬ</div>
        <div class="history-title">ВАША <span class="highlight">ИСТОРИЯ</span></div>
      </div>

      <div class="image-row section">
        <img class="image-1" src="../assets/image 7.jpg" alt="Image 1" />
        <img class="image-2" src="../assets/image 5.jpg" alt="Image 2" />
        <img class="image-3" src="../assets/image 6.jpg" alt="Image 3" />
      </div>

      <div class="section">
        <div class="flex-section">
          <p class="flex-section-text"><span class="highlight">ПОДБОР</span> ЦВЕТОВОЙ ПАЛИТРЫ И <span class="highlight">РЕКОМЕНДАЦИИ</span> ПО ФАСОНАМ И СТИЛЯМ ОДЕЖДЫ</p>
          <div class="flex-section-img"><img id="flex-section-img-1" src="../assets/image 9.png" alt="Image 1" /></div>
        </div>
        <div class="flex-section">
          <div class="flex-section-img"><img id="flex-section-img-2" src="../assets/newspaper.png" alt="Image 2" /></div>
          <p class="flex-section-text"><span class="highlight">НОВОСТИ</span> О ТРЕНДАХ И <span class="highlight">СОВЕТЫ</span> ПО СТИЛЮ</p>
        </div>
        <div class="flex-section">
          <p class="flex-section-text"><span class="highlight">СОХРАНЕНИЕ</span> ПОНРАВИВШИХСЯ КОМБИНАЦИЙ</p>
          <div class="flex-section-img"><img id="flex-section-img-3" src="../assets/vector.png" alt="Image 3" /></div>
        </div>
      </div>
    </div>
  </q-page>
</template>

<script setup>
import { useQuasar } from 'quasar'
import { onMounted, watch } from 'vue'

defineOptions({
  name: 'IndexPage'
});

const $q = useQuasar()

// Initialize dark mode based on system preference
onMounted(() => {
  $q.dark.set('auto')
})

// Watch for dark mode changes
watch(() => $q.dark.isActive, val => {
  console.log(val ? 'Dark mode enabled' : 'Light mode enabled')
})
</script>

<style lang="scss" scoped>
@import '../css/pages/index-page.scss';

:deep(.q-page) {
  background: var(--q-primary-bg);
  transition: background-color 0.3s ease;
}
</style>
