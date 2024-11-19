<template>
  <q-header reveal class="header">
    <q-toolbar>
      <q-toolbar-title class="styled-title">
        COUTURIZE
      </q-toolbar-title>

      <q-btn
        flat
        dense
        round
        :icon="$q.dark.isActive ? 'light_mode' : 'dark_mode'"
        @click="toggleDarkMode"
        class="q-mr-sm theme-toggle"
      />
      
      <q-btn
        flat
        dense
        round
        icon="menu"
        aria-label="Menu"
        @click="$emit('toggle-right-drawer')"
        class="menu-btn"
      />
    </q-toolbar>
  </q-header>
</template>

<script setup>
import { useQuasar } from 'quasar'

defineOptions({
  name: 'HeaderMain'
})

const $q = useQuasar()

const toggleDarkMode = () => {
  $q.dark.toggle()
}
</script>

<style lang="scss" scoped>
.header {
  background: var(--bg-color) !important;
}

.styled-title {
  color: var(--text-color);
  text-transform: uppercase;
  font-size: 54px;
  font-family: var(--font-family);
  letter-spacing: 1px;

  &::first-letter {
    color: var(--highlight-color);
  }
}

.theme-toggle,
.menu-btn {
  color: var(--text-color);
}

@media (max-width: 750px) {
  .styled-title {
    font-size: 44px;
  }
}
@media (max-width: 400px) {
  .styled-title {
    font-size: 34px;
  }
}
</style>
