<template>
  <div class="header">
    <div class="header-container">
      <vz-icon-logo />
      <div class="header-container-menu">
        <span class="header-container-menu-phone" v-text="'+7 812 389 21 12'" />
        <span
          class="header-container-menu-personal"
          v-text="'Личный кабинет'"
        />
      </div>
    </div>
  </div>
</template>

<script>
import VzIconLogo from './icons/vz-icon-logo'
export default {
  name: 'Header',
  components: { VzIconLogo },
}
</script>
