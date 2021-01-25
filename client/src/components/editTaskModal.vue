<template>
  <v-row justify="center">
    <v-dialog
      v-model="active"
      persistent
      max-width="600px"
    >
      <v-card>
        <v-card-title>
          <span class="headline">Edit the task</span>
        </v-card-title>
        <v-card-text>
          <v-container>
            <v-row>
              <v-col
                cols="12"
              >
                <v-text-field
                  label="Task title"
                  required
                  v-model="newTaskTitle"
                ></v-text-field>
              </v-col>

              <v-col cols="12">
                <v-text-field
                  label="Task description"
                  required
                  v-model="newTaskDescription"
                ></v-text-field>
              </v-col>
            </v-row>
          </v-container>
        </v-card-text>
        <v-card-actions>
          <v-spacer></v-spacer>
          <v-btn
            color="primary"
            text
            @click="closeModal"
          >
            Cancel
          </v-btn>
          <v-btn
            color="primary"
            text
            @click="editTask"
          >
            Edit
          </v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
  </v-row>
</template>

<script>
export default {
  props: {
    active: {
      type: Boolean,
      required: true
    },
    title: {
      type: String,
      required: false
    },
    description: {
      type: String,
      required: false
    }
  },
  computed: {
    newTaskTitle: {
      get () {
        return this.title
      },
      set (newVal) {
        this.$emit('update:title', newVal)
      }
    },
    newTaskDescription: {
      get () {
        return this.description
      },
      set (newVal) {
        this.$emit('update:description', newVal)
      }
    }
  },
  methods: {
    closeModal () {
      this.$emit('close')
    },
    editTask () {
      this.$emit('editTask', this.newTaskTitle, this.newTaskDescription)
      this.closeModal()
    }
  }
}
</script>
