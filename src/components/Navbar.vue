<template>
  <header class="header">
    <transition name="header__notes" mode="out-in">
      <nav class="header__nav" v-if="header">
        <button class="header__nav-lang" @click="switchLang">{{$i18n.locale}}</button>
        <h1 class="header__nav-title">{{$t('notes')}}</h1>
        <button class="header__nav-search" @click="header = false">
          <img src="@/assets/images/search.svg" alt="" />
        </button>
      </nav>
      <nav class="header__search" v-else>
        <button class="header__search-back" @click="; (header = true), (search = '')">
          <img src="@/assets/images/back.svg" alt="" />
        </button>
        <input type="text" v-model="search" class="header__search-input" :placeholder="$t('searchInput')" />
        <button class="header__search-clear" @click="search = ''">
          <img src="@/assets/images/clear.svg" alt="" />
        </button>
      </nav>
    </transition>
  </header>
</template>

<script>
export default {
  data() {
    return {
      header: true,
      search: '',
    }
  },
  watch: {
    search(val) {
      this.$emit('setSearch', val)
    }
  },
  methods:{
    switchLang(){
       this.$i18n.locale == 'ru' ? this.$i18n.locale = 'uz' : this.$i18n.locale = 'ru'
    }
  }
}
</script>
