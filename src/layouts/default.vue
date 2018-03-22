<template>
  <q-layout view="lHh Lpr lFf">
    <q-layout-header>
      <q-toolbar color="primary">
        <q-toolbar-title>
          ToDo MVC
        </q-toolbar-title>
        <q-btn flat round dense icon="fab fa-github" size="20px"/>
      </q-toolbar>
    </q-layout-header>
    <q-page-container>
      <router-view />
    </q-page-container>
    <q-layout-footer>
      <q-toolbar color="primary" inverted>
        <q-toolbar-title>
          <span slot="subtitle">
            Application made with <a href="http://quasar-framework.org/" target="blanck">Quasar Framework</a>. For more informations acess the <a href="https://github.com/leochrisis/todoMVC-challenge" target="blanck">Github</a> repository
          </span>
        </q-toolbar-title>
      </q-toolbar>
    </q-layout-footer>
  </q-layout>
</template>

<script>
import { openURL } from 'quasar'

export default {
  name: 'LayoutDefault',
  data () {
    return {
      leftDrawerOpen: this.$q.platform.is.desktop
    }
  },
  methods: {
    openURL
  }
}
</script>

<style>
</style>
