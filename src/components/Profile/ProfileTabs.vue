<template>
  <q-tabs align="left" v-model="tab" class="primary">
<!--    <q-route-tab clickable to="/" name="habits" :label="tabHabitsLabel">-->
<!--    </q-route-tab>-->

    <q-route-tab
      push
      to="/followers"
      name="followers"
      label="Employees">
    </q-route-tab>
<!--    <q-route-tab-->
<!--      clickable-->
<!--      to="following"-->
<!--      name="following"-->
<!--      label="Following (7)"-->
<!--    >-->
<!--    </q-route-tab>-->
  </q-tabs>
</template>

<script>
import { mapState } from "vuex";

export default {
  computed: {
    ...mapState("habits", ["totalHabits"]),
    tabHabitsLabel() {
      return "User tasks (" + this.totalHabits + ")";
    }
  },
  data() {
    return {
      tab: "habits"
    };
  }
};
</script>
