<template>
  <q-layout view="lHh lpr lFf" class="main-bg-color">
    <HeaderMain @toggle-right-drawer="toggleRightDrawer" />

    <q-drawer
      v-model="rightDrawerOpen"
      show-if-above
      side="right"
      :class="$q.dark.isActive ? 'drawer-dark' : 'drawer-light'"
    >
      <q-list>
        <q-item-label header class="drawer-header">
          Меню
        </q-item-label>

        <EssentialLink
          v-for="link in linksList"
          :key="link.title"
          v-bind="link"
          :active="$route.path === link.link"
        />
      </q-list>
    </q-drawer>

    <q-page-container>
      <router-view />
    </q-page-container>
    <FooterMain />
  </q-layout>
</template>

<script setup>
import { ref, computed } from 'vue'
import { useRoute } from 'vue-router'
import EssentialLink from 'components/EssentialLink.vue'
import FooterMain from 'components/FooterMain.vue'
import HeaderMain from 'components/HeaderMain.vue'

defineOptions({
  name: 'MainLayout',
})

const route = useRoute()

const linksList = [
  {
    title: 'Главная страница',
    caption: '',
    link: '/'
  },
  {
    title: 'Подобрать стиль',
    caption: '',
    link: '/style'
  },
  {
    title: 'Просто кнопка',
    caption: '',
    link: '/button'
  },
  {
    title: 'Личный кабинет',
    caption: '',
    link: '/account'
  }
]

const rightDrawerOpen = ref(false)

function toggleRightDrawer() {
  rightDrawerOpen.value = !rightDrawerOpen.value
}
</script>

<style lang="scss">
/* Using global styles to override Quasar's classes */
.q-drawer {
  &.drawer-light {
    background: var(--bg-color) !important;
    color: var(--text-color) !important;
    border-left: 2px solid var(--highlight-color);
  }

  &.drawer-dark {
    background: var(--bg-color) !important;
    color: var(--text-color) !important;
    border-left: 2px solid var(--highlight-color);
  }

  .q-item {
    font-size: 1.5rem !important;
    padding: 1rem !important;
    font-family: var(--font-family) !important;
    color: var(--text-color) !important;
    min-height: unset !important;
    transition: all 0.3s ease !important;

    &:hover {
      background: rgba(var(--highlight-color-rgb), 0.15) !important;
      color: var(--highlight-color) !important;
    }

    &--active {
      background: var(--highlight-color) !important;
      color: white !important;

      &:hover {
        background: rgba(var(--highlight-color-rgb), 0.8) !important;
      }
    }
  }

  .q-item__label--header {
    font-size: 2rem !important;
    padding: 1.5rem 1rem !important;
    color: var(--highlight-color) !important;
    font-family: var(--font-family) !important;
  }
}
</style>
