<template>
  <div id="app">
    <AppTemplate
      applicationName="Current consumption"
      v-bind:navigation="navigation"/>
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
      navigation: [
        {label: 'Current', icon: 'banana', route: '/'},
        {label: 'History', icon: 'banana', route: '/History'},
      ]
    }
  }
}
</script>
<style>

</style>
