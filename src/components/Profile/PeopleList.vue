<template>
  <q-page>
    <div class="q-pa-md">
      <q-markup-table>
        <thead>
        <tr>
          <th colspan="5">
            <div class="row no-wrap items-center">
              <q-img
                style="width: 70px"
                :ratio="1"
                class="rounded-borders"
                src="https://cdn.quasar.dev/img/donuts.png"
              />
              <div class="text-h4 q-ml-md text-white">Employees</div>
            </div>
          </th>
        </tr>
        <tr>
          <th class="text-left">Name</th>
          <th class="text-right">Surname</th>
          <th class="text-right">MobileNumber</th>
          <th class="text-right">Position</th>
          <th class="text-right">Status</th>
          <th class="text-right">Password</th>
          <th class="text-right">Actions</th>
        </tr>
        </thead>
        <tbody>
        <tr
          v-for="(task, key) in tasksTodo"
          :key="key"
          :task="task"
          :id="key"
        >
          <td class="text-left">{{task.name}}</td>
          <td class="text-right">{{task.surname}}</td>
          <td class="text-right">{{task.mobileNumber}}</td>
          <td class="text-right">{{task.position}}</td>
          <td class="text-right">{{task.status}}</td>
          <td class="text-right">{{task.password}}</td>


          <td class="text-right">
            <q-btn
              @click.stop="showEditTaskModal()"
              flat
              round
              dense
              color="primary"
              icon="edit" />
            <q-btn
              @click.stop="promptToDelete(key)"
              flat
              round
              dense
              color="red"
              icon="delete" />
          </td>
        </tr>
        </tbody>
      </q-markup-table>
    </div>

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



    <q-dialog v-model="showEditTask">
      <edit-task
        @close="showEditTask = false"
        :task="task"
        :id="id"
      />
    </q-dialog>



  </q-page>
</template>

<script>
    import { mapActions, mapGetters } from 'vuex'
    export default {
        props: ['task', 'id'],
        data() {
            return {
                showAddTask: false,
                showEditTask: false
            }
        },
        computed: {
            ...mapGetters('tasks', ['tasksTodo'])
        },
        methods: {
            ...mapActions('tasks', ['updateTask', 'deleteTask']),
            showEditTaskModal() {
                this.showEditTask = true
            },
            promptToDelete(id) {
                this.$q.dialog({
                    title: 'Confirm',
                    message: 'Really delete?',
                    ok: {
                        push: true
                    },
                    cancel: {
                        color: 'negative'
                    },
                    persistent: true
                }).onOk(() => {
                    this.deleteTask(id)
                })
            }
        },
        mounted() {
            this.$root.$on('showAddTask', () => {
                this.showAddTask = true
            })
        },
        components: {
             'add-task' : require('components/AddTask2.vue').default,
        }
    }
</script>

<style scoped>

</style>
