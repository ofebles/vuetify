<template>
  <v-menu
    attach
    bottom
    lazy
    left
    offset-y
  >
    <v-btn
      slot="activator"
      flat
      style="min-width: 48px"
      aria-label="Translations"
    >
      <v-img
        :src="`https://cdn.vuetifyjs.com/images/flags/${currentLanguage.country}.png`"
        width="26px"
      />
    </v-btn>
    <v-list
      dense
      light
    >
      <v-list-tile
        v-for="language in languages"
        :key="language.locale"
        avatar
        @click="translateI18n(language.locale)"
      >
        <v-list-tile-avatar
          tile
          size="24px"
        >
          <v-img
            :src="`https://cdn.vuetifyjs.com/images/flags/${language.country}.png`"
            width="24px"
          />
        </v-list-tile-avatar>
        <v-list-tile-title v-text="language.name" />
      </v-list-tile>
    </v-list>
  </v-menu>
</template>

<script>
  // Utilities
  import languages from '@/data/i18n/languages.json'

  export default {
    data: () => ({
      languages
    }),

    computed: {
      currentLanguage () {
        return this.languages.find(l => l.locale === this.$i18n.locale)
      }
    },

    methods: {
      translateI18n (lang) {
        this.$router.replace({ params: { lang } })
        document.cookie = `currentLanguage=${lang};path=/;max-age=${60 * 60 * 24 * 7}` // expires in 7 days
      }
    }
  }
</script>
