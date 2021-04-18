<template>
  <b-input-group class="sections-form-container-list-item-input_group">
    <b-input-group-prepend
      class="sections-form-container-list-item-input_group-code"
    >
      <b-dd
        :lazy="true"
        toggle-class="sections-form-container-list-item-input_group-code-dropdown"
        variant="link"
        boundary="viewport"
        no-caret
        @hidden="toggleDropdown(false)"
        @shown="toggleDropdown(true)"
      >
        <template
          #button-content
          class="sections-form-container-list-item-input_group-code-dropdown-head"
        >
          <span
            class="sections-form-container-list-item-input_group-code-dropdown-head-title"
            v-text="activeCode"
          />
          <i
            class="sections-form-container-list-item-input_group-code-dropdown-head-chevron"
          >
            <b-icon-chevron-up
              v-if="phoneCodeModalIsOpen"
              variant="secondary"
            />
            <b-icon-chevron-down v-else variant="secondary" />
          </i>
        </template>
        <div
          class="sections-form-container-list-item-input_group-code-dropdown-items"
        >
          <b-dd-item-btn
            v-for="(code, key) in codesList"
            :key="key"
            :active="key === activeCode"
            @click="setCountryCode(code)"
          >
            <span
              class="sections-form-container-list-item-input_group-code-dropdown-items-item"
              v-text="code"
            />
          </b-dd-item-btn>
        </div>
      </b-dd>
    </b-input-group-prepend>
    <b-form-input
      v-model="valueCopy"
      type="phone"
      class="sections-form-container-list-item-input_group-input"
      placeholder="(###) ### ####"
    />
  </b-input-group>
</template>
<script>
export default {
  name: 'PhoneInput',
  props: {
    value: {
      type: String,
      default: null,
    },
  },
  data() {
    return {
      phoneCodeModalIsOpen: false,
      activeCode: '+7',
      phone: null,
      codes: ['+7', '+345'],
    }
  },
  computed: {
    valueCopy: {
      get() {
        return this.value
      },
      set(newValue) {
        this.$emit('set-phone', newValue)
      },
    },
    codesList() {
      return this.codes.filter((code) => code !== this.activeCode)
    },
  },
  methods: {
    toggleDropdown(flag) {
      this.phoneCodeModalIsOpen = flag
    },
    setCountryCode(code) {
      this.activeCode = code
    },
  },
}
</script>
