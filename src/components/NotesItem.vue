<template>
  <div class="notes__item">
    <div class="notes__item-top" :class="{ between: !view }">
      <h2 class="notes__item-top-title">{{ note.title }}</h2>
      <p class="notes__item-top-date">{{ note.date }}</p>
    </div>
    <p class="notes__item-text">
      {{ note.text }}
    </p>
    <div class="notes__item-btns">
      <button class="notes__item-btns-btn edit" @click="$emit('change', note.id)">
        <img src="@/assets/images/edit.svg" alt="" />
        <span>{{ $t('edit') }}</span>
      </button>
      <button class="notes__item-btns-btn del" @click="$emit('delNote', note.id)">
        <img src="@/assets/images/del.svg" alt="" />
        <span>{{ $t('del') }}</span>
      </button>
    </div>
  </div>
</template>
<script>
export default {
  props: {
    note: Object,
    view: Boolean,
  },
  data() {
    return {

    }
  }
}
</script>

<style lang="scss" scoped></style>
