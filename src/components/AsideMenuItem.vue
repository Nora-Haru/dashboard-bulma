<template>
  <li :class="{'is-active':isDropdownActive}">
    <component
      :is="componentIs"
      :to="item.to"
      :href="item.href"
      :target="item.target"
      exact-active-class="is-active"
      :class="{'has-icon':!!item.icon}"
      @click="menuClick"
    >
      <b-icon
        v-if="item.icon"
        :icon="item.icon"
        :class="{ 'has-update-mark' : item.updateMark }"
        custom-size="default"
      />
      <span
        v-if="item.label"
        :class="{'menu-item-label':!!item.icon}"
      >{{ item.label }}</span>
    </component>
    <aside-menu-list
      v-if="hasDropdown"
      :menu="item.menu"
      :is-submenu-list="true"
    />
  </li>
</template>

<script>
import { defineComponent } from '@vue/composition-api'

export default defineComponent({
  name: 'AsideMenuItem',
  components: {
    AsideMenuList: () => import('@/components/AsideMenuList.vue')
  },
  props: {
    item: {
      type: Object,
      default: null
    }
  },
  data () {
    return {
      isDropdownActive: false
    }
  },
  computed: {
    componentIs () {
      return this.item.to ? 'router-link' : 'a'
    },
    hasDropdown () {
      return !!this.item.menu
    }
  },
  methods: {
    menuClick () {
      this.$emit('menu-click', this.item)

      if (this.hasDropdown) {
        this.isDropdownActive = (!this.isDropdownActive)
      }
    }
  }
})
</script>
