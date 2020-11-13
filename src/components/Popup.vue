<template>
  <v-dialog max-width="600px">
    <template v-slot:activator="{ on, attrs }">
      <v-btn class="success" text v-bind="attrs" v-on="on"> click</v-btn>
    </template>
    <v-card>
      <v-card-title>
        <h2>Add a new Project</h2>
      </v-card-title>
      <v-card-text>
        <v-form class="px-3">
          <v-text-field
            label="Title"
            v-model="title"
            prepend-icon="mdi-folder"
          ></v-text-field>
          <v-textarea
            label="Information"
            v-model="content"
            prepend-icon="mdi-pencil"
          ></v-textarea>
          <v-menu>
            <template v-slot:activator="{ on, attrs }">
              <v-text-field
                :value="formattedDate"
                label="Picker in menu"
                prepend-icon="mdi-calendar"
                readonly
                v-bind="attrs"
                v-on="on"
              ></v-text-field>
            </template>
            <v-date-picker v-model="due"> </v-date-picker>
          </v-menu>
          <v-btn text class="success mx-0 mt-3" @click="submit"
            >Add project</v-btn
          >
        </v-form>
      </v-card-text>
    </v-card>
  </v-dialog>
</template>

<script>
import format from "date-fns/format";
import parseISO from "date-fns/parseISO";

export default {
  data() {
    return {
      title: "",
      content: "",
      due: null,
    };
  },
  methods: {
    submit() {
      //   console.log(this.title, this.content);
      alert(`${this.title} ${this.content}`);
    },
  },
  computed: {
    formattedDate() {
      return this.due ? format(parseISO(this.due), "do MMM yyyy") : "";
    },
  },
};
</script>
