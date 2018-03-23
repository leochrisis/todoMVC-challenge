<template>
  <div>
    <q-page class="layout-padding">
      <div class="row justify-center">
        <div style="width: 500px; max-width: 90vw;">
          <q-input
            v-model="newTask"
            float-label="Add a new task"
            placeholder="Title"
            v-on:keyup.13="submit"
          />
        </div>
        <div v-if="newTask.length > 0">
          <q-btn round color="primary" icon="create" size="15px"/>

      <div class="row justify-center layout-padding">
        <div style="width: 700px; max-width: 90vw;">
          <div v-for="task in tasks">
            <q-card color="purple-2">
              <q-card-title>
                {{task.title}}
              </q-card-title>
              <q-card-separator />
              <q-card-main>
                {{task.description}}
              </q-card-main>
            </q-card>
            <br>
          </div>
        </div>
      </div>
    </q-page>
  </div>
</template>

<script type="text/javascript">
export default {
  name: 'Home',

  data: () => ({
    newTask: ''
    description: '',
    tasks: []
  }),

  methods: {
    submit () {
      console.log('Hello')
    }
  }
}
</script>
