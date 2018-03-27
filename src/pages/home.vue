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
                float-label= "Add description"
                placeholder="Task description (optional)"
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
          <div v-for="(task,i) in tasks" :key="i">
            <q-card color="purple-2">
              <q-card-title>
                <div v-if="editedIndex ===  i">
                  <q-input
                    v-model="task.title"
                    placeholder="Title"
                    v-on:keyup.13="updateTask"
                  />
                </div>
                <div v-else>
                  <q-checkbox v-model="done" :val="task" @input="doUndoTask(i)"/>
                  <span :class="{undeline: task.done}">{{task.title}}</span>
                </div>
                <q-btn round flat icon="more_vert" slot="right">
                  <q-popover>
                    <q-list link class="no-border" v-if="editedIndex !== i">
                      <q-item v-close-overlay >
                        <q-item-main label="Edit" @click.native="openEditionArea(i)"/>
                      </q-item>
                      <q-item v-close-overlay>
                        <q-item-main label="Delete" @click.native="deleteTask(i)" />
                      </q-item>
                    </q-list>
                    <q-list link class="no-border" v-if="editedIndex === i">
                      <q-item v-close-overlay >
                        <q-item-main label="Finish" @click.native="updateTask(i)" />
                      </q-item>
                      <q-item v-close-overlay>
                        <q-item-main label="Cancel" @click.native="editedIndex = false"/>
                      </q-item>
                    </q-list>
                  </q-popover>
                </q-btn>
              </q-card-title>
              <q-card-separator v-if="task.description.length > 0" />
              <q-card-main>
                <div v-if="editedIndex === i">
                  <q-input
                    v-model="task.description"
                    placeholder="Task description (optional)"
                    v-on:keyup.13="updateTask"
                  />
                </div>
                <div v-else>
                  <span :class="{undeline: task.done}"> {{task.description}} </span>
                </div>
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
    tasks: [],
    done: [],
    editedIndex: false
  }),

  methods: {
    AddNewTask () {
      if (this.title.length !== 0) {
        this.tasks.push({
          title: this.title,
          description: this.description,
          done: false
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
    },

    doUndoTask (index) {
      if (this.tasks[index].done) {
        this.tasks[index].done = false
      } else {
        this.tasks[index].done = true
      }
    },

    openEditionArea (index) {
      this.editedIndex = index
    },

    updateTask () {
      this.editedIndex = false
      this.$q.notify({
        message: `Sucessfuly edited :)`,
        timeout: 1000,
        type: 'positive',
        position: 'top-right'
      })
    },

    deleteTask (index) {
      this.tasks.splice(index, 1)
    }
  }
}
</script>

<style lang="sass">
.undeline
  text-decoration: line-through
</style>
