<template>
  <v-dialog max-width="600px" v-model="dialog">
    <template v-slot:activator="{ on, attrs }">
      <v-btn class="success" text v-bind="attrs" v-on="on"> click</v-btn>
    </template>
    <v-card>
      <v-card-title>
        <h2>Add a new Project</h2>
      </v-card-title>
      <v-card-text>
        <v-form class="px-3" ref="form">
          <v-text-field
            label="Title"
            v-model="title"
            prepend-icon="mdi-folder"
            :rules="inputRules"
          ></v-text-field>
          <v-textarea
            label="Information"
            v-model="content"
            prepend-icon="mdi-pencil"
            :rules="inputRules"
          ></v-textarea>
          <v-menu>
            <template v-slot:activator="{ on, attrs }">
              <v-text-field
                :value="formattedDate"
                label="Picker in menu"
                prepend-icon="mdi-calendar"
                readonly
                :rules="inputRules"
                v-bind="attrs"
                v-on="on"
              ></v-text-field>
            </template>
            <v-date-picker v-model="due"> </v-date-picker>
          </v-menu>
          <v-spacer></v-spacer>
          <v-btn
            text
            class="success mx-0 mt-3"
            @click="submit"
            :loading="loading"
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
import db from "./../firebase";

export default {
  data() {
    return {
      title: "",
      content: "",
      due: null,
      inputRules: [(v) => v.length >= 3 || "Minimum length in 3 characters"],
      loading: false,
      dialog: false,
    };
  },
  methods: {
    submit() {
      //   console.log(this.title, this.content);
      if (this.$refs.form.validate()) {
        this.loading = true;
        // alert(`${this.title} ${this.content}`);
        const project = {
          title: this.title,
          content: this.content,
          due: format(parseISO(this.due), "do MMM yyyy"),
          person: "Karen",
          status: "ongoing",
        };
        db.collection("projects")
          .add(project)
          .then((data) => {
            console.log(data);
            this.loading = false;
            this.dialog = false;
            this.$emit("projectAdded");
          });
      } else {
        console.error("Formulario con errores");
      }
    },
  },
  computed: {
    formattedDate() {
      return this.due ? format(parseISO(this.due), "do MMM yyyy") : "";
    },
  },
};
</script>
