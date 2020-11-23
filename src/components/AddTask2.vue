<template>
  <q-card>
    <q-card-section class="row">
      <div class="text-h6">Add Person</div>
      <q-space />
      <q-btn
        v-close-popup
        flat
        round
        dense
        icon="close" />
    </q-card-section>
    <form
      style="width: 300px;"
      @submit.prevent="submitForm"
      @reset="onReset"
    >
      <q-card-section>
        <div class="row q-mb-sm">
          <q-input
            style="width: 300px;"
            outlined
            v-model="taskToSubmit.name"
            :rules="[val => !!val || 'Field is required']"
            autofocus
            ref="name"
            label="Person name"
            class="col">
            <template v-slot:append>
              <q-icon
                v-if="taskToSubmit.name"
                @click="taskToSubmit.name = ''"
                name="close"
                class="cursor-pointer" />
            </template>
          </q-input>
        </div>
        <div class="row q-mb-sm">
          <q-input
            style="width: 300px;"
            outlined
            ref="surname"
            label="Person surname"
            v-model="taskToSubmit.surname"
            lazy-rules
            :rules="[ val => val && val.length > 0 || 'Please type something']"
          >
            <template v-slot:append>
              <q-icon
                v-if="taskToSubmit.surname"
                @click="taskToSubmit.surname = ''"
                name="close"
                class="cursor-pointer" />
            </template>
          </q-input>
        </div>
        <div class="row q-mb-sm">
          <q-input
            style="width: 300px;"
            outlined
            ref="surname"
            label="Person password"
            v-model="taskToSubmit.password"
            lazy-rules
            :rules="[ val => val && val.length > 0 || 'Please type something']"
          >
            <template v-slot:append>
              <q-icon
                v-if="taskToSubmit.password"
                @click="taskToSubmit.password = ''"
                name="close"
                class="cursor-pointer" />
            </template>
          </q-input>
        </div>
        <div class="row q-mb-sm">
          <q-input
            style="width: 300px;"
            outlined
            ref="surname"
            label="Person mobileNumber"
            v-model="taskToSubmit.mobileNumber"
            lazy-rules
            :rules="[ val => val && val.length > 0 || 'Please type something']"
          >
            <template v-slot:append>
              <q-icon
                v-if="taskToSubmit.mobileNumber"
                @click="taskToSubmit.mobileNumber = ''"
                name="close"
                class="cursor-pointer" />
            </template>
          </q-input>
        </div>

        <div class="row q-mb-sm">
          <q-input
            style="width: 300px;"
            outlined
            ref="surname"
            label="Person position"
            v-model="taskToSubmit.position"
            lazy-rules
            :rules="[ val => val && val.length > 0 || 'Please type something']"
          >
            <template v-slot:append>
              <q-icon
                v-if="taskToSubmit.position"
                @click="taskToSubmit.position = ''"
                name="close"
                class="cursor-pointer" />
            </template>
          </q-input>
        </div>

        <div class="row q-mb-sm">
          <q-input
            style="width: 300px;"
            outlined
            ref="surname"
            label="Person status"
            v-model="taskToSubmit.status"
            lazy-rules
            :rules="[ val => val && val.length > 0 || 'Please type something']"
          >
            <template v-slot:append>
              <q-icon
                v-if="taskToSubmit.status"
                @click="taskToSubmit.status = ''"
                name="close"
                class="cursor-pointer" />
            </template>
          </q-input>
        </div>



      </q-card-section>
      <q-card-actions align="right">
        <q-btn
          label="Save"
          color="primary"
          type="submit" />
        <q-btn label="Reset" type="reset" color="primary" flat class="q-ml-sm" />
      </q-card-actions>
    </form>

  </q-card>
</template>

<script>
    import { mapActions } from 'vuex'


    export default {
        data() {
            return {
                taskToSubmit: {
                    name: '',
                    surname: '',
                    mobileNumber: '',
                    position: '',
                    status: '',
                    password: '',
                }
            }
        },
        methods: {
            ...mapActions('tasks', ['addTask']),
            submitForm() {
                this.$refs.name.validate()
                this.$refs.surname.validate()
                if (!this.$refs.name.hasError && !this.$refs.surname.hasError) {
                    this.submitTask()
                }
            },
            submitTask() {
                this.addTask(this.taskToSubmit)
                this.$emit('close')
            },
            onReset () {
                this.taskToSubmit.name = null
                this.taskToSubmit.surname = null
                this.taskToSubmit.model = null
                this.taskToSubmit.gender = null
                this.taskToSubmit.customModel = null
            }
        }
    }
</script>
