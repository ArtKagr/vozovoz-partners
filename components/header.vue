<template>
  <div class="header">
    <div class="header-container">
      <vz-icon-logo class="header-container-logo" />
      <div class="header-container-menu">
        <div class="header-container-menu-phone">
          <b-dd
            :lazy="true"
            toggle-class="header-container-menu-phone-dropdown"
            variant="link"
            boundary="viewport"
            no-caret
            @hidden="toggleDropdown(false)"
            @shown="toggleDropdown(true)"
          >
            <template
              #button-content
              class="header-container-menu-phone-dropdown-head"
            >
              <span
                class="header-container-menu-phone-dropdown-head-title"
                v-text="'+7 812 389 21 12'"
              />
              <i class="header-container-menu-phone-dropdown-head-chevron">
                <b-icon-chevron-up
                  v-if="phoneModalIsOpened"
                  variant="secondary"
                />
                <b-icon-chevron-down v-else variant="secondary" />
              </i>
            </template>
          </b-dd>
        </div>
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
  data() {
    return {
      phoneModalIsOpened: false,
    }
  },
  methods: {
    toggleDropdown(flag) {
      this.phoneModalIsOpened = flag
    },
  },
}
</script>
