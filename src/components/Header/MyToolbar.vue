<template>
  <q-toolbar class="test">
    <q-btn
      color="white"
      class="absolute-top-center"
      flat
      round
      @click="$q.dark.toggle()"
      :icon="$q.dark.isActive ? 'nights_stay' : 'wb_sunny'"
    />

    <q-space />



    <dropdown-settings v-if="loggedIn" />
  </q-toolbar>
</template>

<script>
import { mapState } from "vuex";

export default {
  computed: {
    ...mapState("auth", ["loggedIn"])
  },
  components: {
    "dropdown-settings": require("src/components/Header/DropdownSettings.vue")
      .default
  }
};
</script>

<style>
.q-btn__wrapper {
  padding: 2px 8px !important;
}

.self-stretch {
  align-self: stretch;
}
</style>
