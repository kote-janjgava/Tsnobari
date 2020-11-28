<template>
  <q-page class="q-pa-md">
      <List
        v-for="(task, key) in people"
        :key="key"
        :task="task"
        :id="key"></List>
    <div style="position: relative; margin-right: 10px;" class="absolute-bottom text-center q-mb-lg">
      <q-btn
        @click="showAddTask = true"
        round
        color="green"
        size="24px"
        icon="add"
      />
    </div>

    <q-dialog v-model="showAddTask">
      <add-task @close="showAddTask = false" />
    </q-dialog>
  </q-page>
</template>

<script>
    import { mapGetters } from 'vuex'

    export default {
        data() {
            return {
                showAddTask: false
            }
        },
        computed: {
            ...mapGetters('people', ['people'])
        },
        components: {
            'List' : require('components/Tasks/List.vue').default,
            'add-task' : require('components/AddPerson.vue').default,
        }
    }
</script>

<style>

</style>
