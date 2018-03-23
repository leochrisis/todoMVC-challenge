<template>
  <div>
    <q-page class="layout-padding">
      <div class="row justify-center">
        <div style="width: 500px; max-width: 90vw;">
          <q-input
            v-model="title"
            float-label="Add a new task"
            placeholder="Title"
            v-on:keyup.13="AddNewTask"
          />
          <div v-if="title.length > 0">
            <br>
            <q-slide-transition>
              <q-input
                v-model="description"
                float-label= "Task description (optional)"
                placeholder="Title"
                v-on:keyup.13="AddNewTask"
              />
            </q-slide-transition>
            <br>
            <div class="row justify-end">
              <q-slide-transition>
                <q-btn round color="primary" icon="create" size="15px" @click="AddNewTask"/>
              </q-slide-transition>
            </div>
          </div>
        </div>
      </div>

      <div class="row justify-center layout-padding">
        <div style="width: 700px; max-width: 90vw;">
          <div v-for="task in tasks">
            <q-card color="purple-2">
              <q-card-title>
                {{task.title}}
                <q-btn round flat icon="more_vert" slot="right">
                  <q-popover>
                    <q-list link class="no-border">
                      <q-item v-close-overlay>
                        <q-item-main label="Edit task" />
                      </q-item>
                      <q-item v-close-overlay>
                        <q-item-main label="Delete task" />
                      </q-item>
                    </q-list>
                  </q-popover>
                </q-btn>
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
    title: '',
    description: '',
    tasks: []
  }),

  methods: {
    AddNewTask () {
      if (this.title.length !== 0) {
        this.tasks.push({
          title: this.title,
          description: this.description
        })
        this.title = ''
        this.description = ''
        this.$q.notify({
          message: `Sucessfuly added :)`,
          timeout: 1000,
          type: 'positive',
          position: 'top-right'
        })
      } else {
        this.$q.notify({
          message: `Please, insert a task title`,
          timeout: 1000,
          type: 'warning',
          position: 'top-right'
        })
      }
    }
  }
}
</script>
