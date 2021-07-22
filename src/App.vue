<template>
  <div id="app">
    <AppTemplate
      :options="options">
      <template v-slot:nav>
        <router-link to="/">Current</router-link>
        <router-link to="/history">History</router-link>
      </template>
      <router-view />
    </AppTemplate>
  </div>
</template>
<script>

import AppTemplate from '@moreillon/vue_application_template'

export default {
  name: 'App',
  components: {
    AppTemplate,
  },
  data(){
    return {
      options: {
        title: 'Current consumption',
        authenticate: true,
        login_url: `${process.env.VUE_APP_AUTHENTICATION_API_URL}/login`,
        identification_url: `${process.env.VUE_APP_AUTHENTICATION_API_URL}/whoami`
      },
    }
  }
}
</script>
<style>
main {
  padding-top: 3em;
}
</style>
