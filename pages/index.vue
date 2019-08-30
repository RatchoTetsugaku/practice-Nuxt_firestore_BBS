<template>
  <v-app>
    <v-container>
      <BBS />
      <FormForBBS />
    </v-container>
  </v-app>
</template>

<script>
import Logo from '~/components/Logo.vue'
import VuetifyLogo from '~/components/VuetifyLogo.vue'
import BBS from '~/components/BBS.vue'
import FormForBBS from '~/components/FormForBBS.vue'

export default {
  components: {
    Logo,
    VuetifyLogo,
    BBS,
    FormForBBS
  }
}
</script>
