<template>
  <b-modal
    :active.sync="isModalActive"
    has-modal-card
  >
    <div class="modal-card">
      <header class="modal-card-head">
        <p class="modal-card-title">
          Confirm action
        </p>
        <button
          type="button"
          class="delete"
          @click="cancel"
        />
      </header>
      <section class="modal-card-body">
        <p>This will permanently delete <b>{{ trashObjectName }}</b></p>
        <p>Action can not be undone.</p>
      </section>
      <footer class="modal-card-foot">
        <button
          class="button"
          type="button"
          @click="cancel"
        >
          Cancel
        </button>
        <button
          class="button is-danger"
          @click="confirm"
        >
          Delete
        </button>
      </footer>
    </div>
  </b-modal>
</template>

<script>
import { defineComponent } from '@vue/composition-api'

export default defineComponent({
  name: 'ModalBox',
  props: {
    isActive: {
      type: Boolean,
      default: false
    },
    trashObjectName: {
      type: String,
      default: null
    }
  },
  data () {
    return {
      isModalActive: false
    }
  },
  watch: {
    isActive (newValue) {
      this.isModalActive = newValue
    },
    isModalActive (newValue) {
      if (!newValue) {
        this.cancel()
      }
    }
  },
  methods: {
    cancel () {
      this.$emit('cancel')
    },
    confirm () {
      this.$emit('confirm')
    }
  }
})
</script>
