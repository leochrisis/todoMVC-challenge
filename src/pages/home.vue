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
  }),

  methods: {
    submit () {
      console.log('Hello')
    }
  }
}
</script>
