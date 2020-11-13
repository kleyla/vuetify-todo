<template>
  <div class="team">
    <h1 class="subheading grey--text">Team</h1>
    <v-container class="my-5">
      <v-row>
        <v-col
          sx="12"
          sm="6"
          md="4"
          lg="3"
          v-for="(person, index) in team"
          :key="index"
        >
          <v-card flat class="text-center ma-3">
            <v-responsive class="pt-4">
              <v-avatar size="100" class="grey lighten-2">
                <img :src="person.avatar" alt="person" />
              </v-avatar>
            </v-responsive>
            <v-card-text>
              <div class="subheading">{{ person.name }}</div>
              <div class="grey--text">{{ person.role }}</div>
            </v-card-text>
            <v-card-actions>
              <v-btn text color="grey">
                <v-icon small>mdi-message</v-icon>
                <span>Message</span>
              </v-btn>
            </v-card-actions>
          </v-card>
        </v-col>
      </v-row>
    </v-container>
  </div>
</template>

<script>
export default {
  data() {
    return {
      team: [
        { name: "Karen", role: "Web developer", avatar: "/me1.jpg" },
        { name: "Yolanda", role: "Graphic designer", avatar: "/me1.jpg" },
        { name: "Andrea", role: "Web developer", avatar: "/me1.jpg" },
        { name: "Juan", role: "Social media maverick", avatar: "/me1.jpg" },
        { name: "Daniel", role: "Sales guru", avatar: "/me1.jpg" },
      ],
    };
  },
};
</script>
