<template>
  <q-layout view="lHh Lpr lFf">
    <q-header elevated>
      <q-toolbar>
        <q-btn
          flat
          dense
          round
          icon="menu"
          aria-label="Menu"
          @click="toggleLeftDrawer"
        />

        <q-toolbar-title>
          Busca CEP
        </q-toolbar-title>

        <div>Quasar v{{ $q.version }}</div>
      </q-toolbar>
    </q-header>

    <q-drawer
      v-model="leftDrawerOpen"
      show-if-above
      bordered
    >
      <q-list>
        <q-item-label
          header
        >
          Links
        </q-item-label>

        <EssentialLink
          v-for="link in linksList"
          :key="link.title"
          v-bind="link"
        />
      </q-list>
    </q-drawer>

    <q-page-container>
      <router-view />
    </q-page-container>
  </q-layout>
</template>

<script setup>
import { ref } from 'vue'
import EssentialLink from 'components/EssentialLink.vue'

const linksList = [
  {
    title: 'Dev',
    caption: 'guilherme.dev',
    icon: 'school',
    link: 'https://quasar.dev'
  },
  {
    title: 'Github',
    caption: 'https://github.com/guilerm3',
    icon: 'code',
    link: 'https://github.com/guilerm3'
  },
  {
    title: 'Whatsapp',
    caption: 'chat.whatsapp.com',
    icon: 'chat',
    link: 'https://api.whatsapp.com/send/?phone=5531988884037&text&type=phone_number&app_absent=0'
  },
  {
    title: 'Instagram',
    caption: '@guiaugusto_22',
    icon: 'rss_feed',
    link: 'https://www.instagram.com/guiaugusto_22/'
  },
  {
    title: 'Linkedin',
    caption: 'linkedin.com/in/guilerm3/',
    icon: 'public',
    link: 'https://www.linkedin.com/in/guilerm3/'
  },
]

const leftDrawerOpen = ref(false)

function toggleLeftDrawer () {
  leftDrawerOpen.value = !leftDrawerOpen.value
}
</script>
