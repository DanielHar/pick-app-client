<template>
  <v-app>
    <v-toolbar app>
      <v-toolbar-title class="headline">
        <span>PickApp</span>
        <span class="font-weight-light ml-3">Choose Locations</span>
      </v-toolbar-title>
      <v-spacer></v-spacer>
      <span class="mr-2">Daniel Harit</span>
    </v-toolbar>
    <v-content>
      <LocationsForm/>
    </v-content>
  </v-app>
</template>

<script>
import LocationsForm from './components/LocationsForm'

export default {
  name: 'App',
  components: {
    LocationsForm
  },
  data () {
    return {
      //
    }
  }
}
</script>
