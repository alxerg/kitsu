<template>
<td class="actions has-text-right">
  <button
    class="button"
    data-test="button-history"
    @click="$emit('history-clicked')"
    v-if="!hideHistory"
  >
    <clock-icon class="icon is-small only-icon" />
  </button>

  <router-link
    class="button"
    data-test="button-edit"
    :to="editRoute"
    v-if="!hideEdit && !entry.canceled"
  >
    <edit-icon class="icon is-small only-icon" />
  </router-link>

  <router-link
    class="button"
    data-test="button-restore"
    :to="restoreRoute"
    v-if="entry.canceled"
  >
    <rotate-ccw-icon class="icon is-small only-icon" />
  </router-link>

  <router-link
    class="button"
    data-test="button-delete-admin"
    :to="deleteRoute"
    v-if="!hideDelete && !entry.canceled && isCurrentUserAdmin"
  >
    <trash-icon class="icon is-small only-icon" />
  </router-link>

  <router-link
    class="button"
    data-test="button-delete"
    :to="deleteRoute"
    v-else-if="!hideDelete"
  >
    <trash-icon class="icon is-small only-icon" />
  </router-link>
</td>
</template>

<script>
import { mapGetters, mapActions } from 'vuex'
import {
  ClockIcon,
  EditIcon,
  RotateCcwIcon,
  TrashIcon
} from 'vue-feather-icons'

export default {
  name: 'row-actions',
  components: {
    ClockIcon,
    EditIcon,
    RotateCcwIcon,
    TrashIcon
  },

  props: {
    entry: {
      type: Object,
      default: () => {
        return {}
      }
    },
    editRoute: {
      type: Object,
      default: () => {
        return { name: 'home' }
      }
    },
    deleteRoute: {
      type: Object,
      default: () => {
        return { name: 'home' }
      }
    },
    restoreRoute: {
      type: Object,
      default: null
    },
    hideEdit: {
      type: Boolean,
      default: false
    },
    hideDelete: {
      type: Boolean,
      default: false
    },
    hideHistory: {
      type: Boolean,
      default: true
    }
  },
  computed: {
    ...mapGetters([
      'isCurrentUserAdmin'
    ])
  },
  methods: {
    ...mapActions([
    ])
  }
}
</script>

<style lang="scss" scoped>
.button {
  margin-left: 0.2em;
}
</style>
