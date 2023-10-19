<template>
  <div class="notes">
    <div class="container">
      <div class="notes__top">
        <h2 class="notes__top-title">{{ notes.length > 0 ?  $t('addNote')  : $t('noNotes') }}</h2>
        <button class="notes__top-btn" @click="view = !view">
          <img src="@/assets/images/list.svg" alt="" v-if="view" />
          <img src="@/assets/images/grid.svg" alt="" v-else />
          <span>{{ view ? $t('list') : $t('grid') }}</span>
        </button>
      </div>
      <div class="notes__list" :class="{ active: !view }">
        <NotesItem v-for="note in notes" :key="note.id" :note="note" :view="view" @change="$emit('change', note.id)"
          @delNote="$emit('delNote', note.id)" />
      </div>
    </div>
  </div>
</template>

<script>
import NotesItem from './NotesItem.vue'

export default {
  props: {
    notes: Array
  },
  components: {
    NotesItem,
  },
  data() {
    return {
      view: true
    }
  },
}
</script>

<style lang="scss" scoped></style>
