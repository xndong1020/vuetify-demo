<template>
  <v-dialog max-width="600px">
    <v-btn flat slot="activator" class="success">Add new project</v-btn>
    <v-card>
      <v-card-title>Add a new project</v-card-title>
      <v-card-text>
        <v-form class="px-3" ref="form">
          <v-text-field label="Title" v-model="title" :rules="inputRules" prepend-icon="folder"></v-text-field>
          <v-textarea label="Information" v-model="content" prepend-icon="edit"></v-textarea>

          <v-menu>
            <v-text-field slot="activator" :value="formattedDue" label="Due date" prepend-icon="date_range">
            </v-text-field>
            <v-date-picker v-model="due"></v-date-picker>
          </v-menu>

          <v-spacer></v-spacer>
          <v-btn flat class="success mx-0 mt-3" @click="submit" :loading="true">Add project</v-btn>
        </v-form>
      </v-card-text>
    </v-card>
  </v-dialog>
</template>

<script>
import moment from 'moment'
export default {
  data() {
    return {
      title: "",
      content: "",
      due: "",
      inputRules: [v => v.length >= 3 || "Minimun length is 3 chars"]
    };
  },
  computed: {
    formattedDue() {
      return this.due ? moment(this.due).format('dddd, MMMM Do YYYY') : ''
    }
  },
  methods: {
    submit() {
      if (this.$refs.form.validate()) {
        console.log("submit", this.title, this.content);
      }
    }
  }
};
</script>

