<template>
  <nav
    v-show="isNavBarVisible"
    id="navbar-main"
    class="navbar is-fixed-top"
  >
    <div class="navbar-brand">
      <a
        class="navbar-item is-hidden-desktop"
        @click.prevent="menuToggleMobile"
      >
        <b-icon :icon="menuToggleMobileIcon" />
      </a>
      <div class="navbar-item has-control">
        <div class="control">
          <input
            class="input"
            placeholder="Search everywhere..."
          >
        </div>
      </div>
    </div>
    <div class="navbar-brand is-right">
      <div class="navbar-item navbar-item-menu-toggle is-hidden-desktop">
        <a @click.prevent="menuNavBarToggle">
          <b-icon
            :icon="menuNavBarToggleIcon"
            custom-size="default"
          />
        </a>
      </div>
    </div>
    <div
      class="navbar-menu fadeIn animated faster"
      :class="{'is-active':isMenuNavBarActive}"
    >
      <div class="navbar-end">
        <nav-bar-menu class="has-user-avatar">
          <div class="is-user-avatar">
            <img
              :src="userAvatar"
              :alt="userName"
            >
          </div>
          <div class="is-user-name">
            <span>{{ userName }}</span>
          </div>

          <div
            slot="dropdown"
            class="navbar-dropdown"
          >
            <router-link
              to="/profile"
              class="navbar-item"
              exact-active-class="is-active"
            >
              <b-icon
                icon="account"
                custom-size="default"
              />
              <span>My Profile</span>
            </router-link>
            <a class="navbar-item">
              <b-icon
                icon="settings"
                custom-size="default"
              />
              <span>Settings</span>
            </a>
            <a class="navbar-item">
              <b-icon
                icon="email"
                custom-size="default"
              />
              <span>Messages</span>
            </a>
            <hr class="navbar-divider">
            <a class="navbar-item">
              <b-icon
                icon="logout"
                custom-size="default"
              />
              <span>Log Out</span>
            </a>
          </div>
        </nav-bar-menu>
        <a
          href="https://github.com/vikdiesel/admin-two-vue-bulma-dashboard"
          target="_blank"
          class="navbar-item"
          title="GitHub"
        >
          <b-icon
            icon="github-circle"
            custom-size="default"
          />
          <span>GitHub</span>
        </a>
        <a
          class="navbar-item"
          title="Log out"
          @click="logout"
        >
          <b-icon
            icon="logout"
            custom-size="default"
          />
          <span>Log out</span>
        </a>
      </div>
    </div>
  </nav>
</template>

<script>
import { defineComponent } from '@vue/composition-api'
import { mapState } from 'vuex'
import NavBarMenu from '@/components/NavBarMenu.vue'

export default defineComponent({
  name: 'NavBar',
  components: {
    NavBarMenu
  },
  data () {
    return {
      isMenuNavBarActive: false
    }
  },
  computed: {
    menuNavBarToggleIcon () {
      return (this.isMenuNavBarActive) ? 'close' : 'dots-vertical'
    },
    menuToggleMobileIcon () {
      return this.isAsideMobileExpanded ? 'backburger' : 'forwardburger'
    },
    ...mapState([
      'userName',
      'userAvatar',
      'isNavBarVisible',
      'isAsideMobileExpanded'
    ])
  },
  mounted () {
    this.$router.afterEach(() => {
      this.isMenuNavBarActive = false
    })
  },
  methods: {
    menuToggleMobile () {
      this.$store.commit('asideMobileStateToggle')
    },
    menuNavBarToggle () {
      this.isMenuNavBarActive = (!this.isMenuNavBarActive)
    },
    logout () {
      this.$buefy.snackbar.open({
        message: 'Log out clicked',
        queue: false
      })
    }
  }
})
</script>
